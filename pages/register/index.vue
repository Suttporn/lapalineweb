<template >
  <div class>
    <b-card
      overlay
      img-src="https://scontent.fbkk5-1.fna.fbcdn.net/v/t1.15752-9/s2048x2048/95496286_2868279806774852_6694756414096670720_n.jpg?_nc_cat=109&_nc_sid=b96e70&_nc_eui2=AeHlMSDoLE_h5z5FTD3D5fhWnCfsW1QIrd-cJ-xbVAit30aq88hpcvkVgE_0_QMbmR4WJlJCfOJPR5410Cd6NuaI&_nc_ohc=t_oQI4K91fkAX8b9dff&_nc_ht=scontent.fbkk5-1.fna&_nc_tp=7&oh=fb0cc570141a136c42efcc3c647327bd&oe=5ED6E790"
      img-alt
      text-variant="white"
      title
      sub-title
    ></b-card>
    <div>
      <!-- onclick="this.style.display = 'none'" -->
      <div>
        <b-card title="สมัครสมาชิก">
          <b-card-text>
            <h5>คำนำหน้า</h5>
            <b-form-select
              v-model="PENAME"
              :options="options1"
              class="mb-3"
              value-field="item"
              text-field="name"
              disabled-field="notEnabled"
            ></b-form-select>
            <h5>ชื่อ</h5>
            <b-form-input v-model="NAME" placeholder="Enter your name"></b-form-input>
            <h5>นามสกุล</h5>
            <b-form-input v-model="LNAME" placeholder="Enter your last name"></b-form-input>
            <h5>เลขบัตรประจำตัวประชาชน</h5>
            <b-form-input v-model="CID" placeholder="Enter your cardnumber"></b-form-input>
            <h5>สถานะ</h5>
            <b-form-select
              v-model="STATUS"
              :options="options3"
              class="mb-3"
              value-field="item"
              text-field="name"
              disabled-field="notEnabled"
            ></b-form-select>
            <h5>รหัสโรงพยาบาล</h5>
            <b-form-input v-model="HOSPCODE" placeholder="Enter your hospital"></b-form-input>
            <h5>ที่อยู่</h5>
            <b-form-input v-model="ADDRESS" placeholder="Enter your address"></b-form-input>
            <h5>เลขที่ผู้ป่วยนอก</h5>
            <b-form-input v-model="HN" placeholder="Enter your Out Patient "></b-form-input>
            <h5>เพศ</h5>
            <b-form-group>
              <b-form-radio v-model="SEX" value="ชาย">ชาย</b-form-radio>
              <b-form-radio v-model="SEX" value="หญิง">หญิง</b-form-radio>
            </b-form-group>
            <h5>วันเกิด</h5>
            <b-form-datepicker id="example-datepicker" v-model="BIRTH" class="mb-2"></b-form-datepicker>
            <h5>เลขบัตรประจำตัวประชาชน บิดา</h5>
            <b-form-input v-model="FATHER" placeholder="Enter your cardnumber father"></b-form-input>
            <h5>เลขบัตรประจำตัวประชาชน มารดา</h5>
            <b-form-input v-model="MOTHER" placeholder="Enter your cardnumber mother"></b-form-input>
            <h5>สถานะ/สาเหตุการจำหน่าย</h5>
            <b-form-select
              v-model="DISCHARGE"
              :options="options2"
              class="mb-3"
              value-field="item"
              text-field="name"
              disabled-field="notEnabled"
            ></b-form-select>
            <h5>วันที่จำหน่าย</h5>
            <b-form-datepicker id="example-datepicker" v-model="DDISCHARGE" class="mb-2"></b-form-datepicker>
            <h5>หมู่เลือด</h5>
            <b-form-group>
              <b-form-radio v-model="ABOGROUP" value="A">A</b-form-radio>
              <b-form-radio v-model="ABOGROUP" value="B">B</b-form-radio>
              <b-form-radio v-model="ABOGROUP" value="O">O</b-form-radio>
              <b-form-radio v-model="ABOGROUP" value="AB">AB</b-form-radio>
            </b-form-group>
            <h5>หมู่เลือด RH</h5>
            <b-form-group>
              <b-form-radio v-model="RHGROUP" value="Positive">Positive</b-form-radio>
              <b-form-radio v-model="RHGROUP" value="Nagative">Nagative</b-form-radio>
            </b-form-group>
            <h5>วันที่ปรับปรุงข้อมูล</h5>
            <b-form-datepicker id="example-datepicker" v-model="D_UPDATE" class="mb-2"></b-form-datepicker>
            <h5>เบอร์โทรศัทพ์</h5>
            <b-form-input v-model="TELEPHONE" placeholder="Enter your phone"></b-form-input>
            <h5>เบอร์โทรศัทพ์มือถือ</h5>
            <b-form-input v-model="MOBILE" placeholder="Enter your mobile"></b-form-input>
            <h5>วันที่เพิ่มข้อมูล</h5>
            <b-form-datepicker id="example-datepicker" v-model="CREATE_DATE" class="mb-2"></b-form-datepicker>
          </b-card-text>
          <b-button pill variant="success" v-b-modal.modalPopover @click="addregister">ยืนยัน</b-button>
        </b-card>
      </div>
    </div>

    <b-modal id="modalPopover" title="QRcode ของคุณ" ok-only onclick="javascript:window.close();">
      <div class="card">
        <b-card>
          <center>
            <qrcode-vue :value="Qrcode+CID" :size="size" level="H"></qrcode-vue>
          </center>
        </b-card>
      </div>
    </b-modal>
  </div>
</template>

<script>
import axios from 'axios'
import QrcodeVue from 'qrcode.vue'

export default {
  head() {
    return {
      script: [{ src: 'https://static.line-scdn.net/liff/edge/2/sdk.js' }],
      link: [
        {
          rel: 'stylesheet',
          href: 'https://fonts.googleapis.com/css?family=Roboto&display=swap'
        }
      ]
    }
  },
  data: () => ({
    options1: [
      { item: 'นาย', name: 'นาย' },
      { item: 'นาง', name: 'นาง' },
      { item: 'นางสาว', name: 'นางสาว' }
    ],
    options2: [
      { item: 'ตาย', name: 'ตาย' },
      { item: 'ย้าย', name: 'ย้าย' },
      { item: 'สาบสูญ', name: 'สาบสูญ' },
      { item: 'ไม่จำหน่าย', name: 'ไม่จำหน่าย' }
    ],
    options3: [
      { item: 'ประชาชนทั่วไป', name: 'ประชาชนทั่วไป' },
      { item: 'อสม', name: 'อสม' },
      { item: 'หมอ', name: 'หมอ' }
    ],

    // cid: 'https://line.me/R/oaMessage/@429qongn/?signin:',
    Qrcode:'https://liff.line.me/1654248577-R3KA8WKD/signin/',

    PENAME: '',
    NAME: '',
    LNAME: '',
    CID: '',
    STATUS: '',
    HOSPCODE: '',
    ADDRESS: '',
    HN: '',
    SEX: '',
    BIRTH: '',
    FATHER: '',
    MOTHER: '',
    DISCHARGE: '',
    DDISCHARGE: '',
    ABOGROUP: '',
    RHGROUP: '',
    D_UPDATE: '',
    TELEPHONE: '',
    MOBILE: '',
    CREATE_DATE: '',
    USERID: '',
    size: 200
  }),
  components: {
    QrcodeVue
  },
  beforeMount() {
    this.GetProfileLine()
  },
  methods: {
    GetProfileLine() {
     
      console.log('1654248577-V4x1eMxG', 'ffff')

      function initializeLiff(myLiffId) {
        liff
          .init({
            liffId: myLiffId
          })
          .then(() => {
            liff.getProfile().then(p => {
              //alert(p.userId)
              this.USERID = p.userId
            })
          })
      }
      initializeLiff('1654248577-R3KA8WKD')
       
    },
    addregister: function(event) {
      var data = {
        PENAME: this.PENAME,
        NAME: this.NAME,
        LNAME: this.LNAME,
        CID: this.CID,
        STATUS: this.STATUS,
        HOSPCODE: this.HOSPCODE,
        ADDRESS: this.ADDRESS,
        HN: this.HN,
        SEX: this.SEX,
        BIRTH: this.BIRTH,
        FATHER: this.FATHER,
        MOTHER: this.MOTHER,
        DISCHARGE: this.DISCHARGE,
        DDISCHARGE: this.DDISCHARGE,
        ABOGROUP: this.ABOGROUP,
        RHGROUP: this.RHGROUP,
        D_UPDATE: this.D_UPDATE,
        TELEPHONE: this.TELEPHONE,
        MOBILE: this.MOBILE,
        CREATE_DATE: this.CREATE_DATE
      }
      axios
        .post('https://lapa-line-bot-api.glitch.me/insert', data)
        .then(response => {
          // this.info = response.data[3]
          console.log(response)
        })
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

