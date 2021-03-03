<template>
  <div>
    <h2>폼</h2>
    <VCheckbox :one-check="true" :checked.sync="checkboxDataVal">단독체크박스</VCheckbox>
    <div>{{checkboxDataVal}}</div>
    <VCheckbox v-model="checkboxListDataVal" :data="checkboxListData"></VCheckbox>
   <div> {{checkboxListDataVal}}</div>

   <!-- <VRadio v-model="radioCheck" :data="optList1" class="inbl"></VRadio>
   <VRadio v-model="optsList2Checked" :data="optList2"
    :custom-label="true"
    value-key="id"
    label-key="label"
   >
    <template slot-scope="props">{{props.item.label}}</template>
   </VRadio> -->
<!-- <el-radio v-model="radioCheck" label="1">Option A</el-radio>
  <el-radio v-model="radioCheck" label="2">Option B</el-radio> -->
   <VRadio v-model="radioCheck" class="inbl" label="1">라디오</VRadio>
   <VRadio v-model="radioCheck" class="inbl" label="2">라디오2</VRadio>
   <div>{{radioCheck}}</div>

   <h2>탭</h2>
   <VTab class="tab-default" :data="tabList" :contents="true">
     <template slot="contents">
       <div style="border:1px solid #000" data-id="tab1">tab1</div>
       <div style="border:1px solid #000" data-id="tab2">tab2</div>
       <div style="border:1px solid #000" data-id="tab3">tab3</div>
     </template>
   </VTab>

   <h2>리스트탭</h2>
    <el-collapse :v-model="1" >
      <el-collapse-item name="1">
         <template slot="title">
          <div>
            Consistency<i class="header-icon el-icon-info"></i>
          </div>
        </template>
        <div>Consistent with real life: in line with the process and logic of real life, and comply with languages and habits that the users are used to;</div>
        <div>Consistent within interface: all elements should be consistent, such as: design style, icons and texts, position of elements, etc.</div>
      </el-collapse-item>
      <el-collapse-item title="Feedback" name="2">
        <div>Operation feedback: enable the users to clearly perceive their operations by style updates and interactive effects;</div>
        <div>Visual feedback: reflect current state by updating or rearranging elements of the page.</div>
      </el-collapse-item>
      <el-collapse-item title="Efficiency" name="3">
        <div>Simplify the process: keep operating process simple and intuitive;</div>
        <div>Definite and clear: enunciate your intentions clearly so that the users can quickly understand and make decisions;</div>
        <div>Easy to identify: the interface should be straightforward, which helps the users to identify and frees them from memorizing and recalling.</div>
      </el-collapse-item>
      <el-collapse-item title="Controllability" name="4">
        <div>Decision making: giving advices about operations is acceptable, but do not make decisions for the users;</div>
        <div>Controlled consequences: users should be granted the freedom to operate, including canceling, aborting or terminating current operation.</div>
      </el-collapse-item>
    </el-collapse>

   <h2>슬라이더</h2>
    <el-slider v-model="sliderVal" @change="chanteSliderVal()"></el-slider>


<el-form :model="checkboxDataVal2" :rules="rules" ref="ruleForm" label-width="120px" class="demo-ruleForm">
      <el-form-item label="Activity type" prop="type2">
    <VCheckbox :one-check="true" error="에러입니다" :checked="checkboxDataVal2.check">단독체크박스</VCheckbox>

     <!-- <el-checkbox v-model="checkboxDataVal2.check">Option</el-checkbox> -->
    <!-- <el-checkbox-group v-model="ruleForm.type">
      <el-checkbox label="Online activities" name="type"></el-checkbox>
      <el-checkbox label="Promotion activities" name="type"></el-checkbox>
      <el-checkbox label="Offline activities" name="type"></el-checkbox>
      <el-checkbox label="Simple brand exposure" name="type"></el-checkbox>
    </el-checkbox-group> -->
    <!-- <VCheckbox v-model="checkboxDataVal2.type" :data="checkboxListData"></VCheckbox> -->
  </el-form-item>
</el-form>  

    <h2>별점</h2>
    <v-rate v-model="rateval"
      >
    <!-- @change="aaa" -->
      <!-- :colors="colors" -->
    </v-rate>
    <div>{{ rateval }}</div>

    <h2>파일첨부</h2>
    <div class="file-upload">
      <div class="file-input">
        <input ref="fileInput" type="file" class="offscreen" @change="changeFile" />
        <v-input v-model="fileVal" class="file-value" />
        <v-btn v-if="fileVal !== ''" class="btn-file-delete" type="button" @click="fileDelete"><span>파일삭제</span></v-btn>
      </div>
      <v-btn class="file-btn btn-more" type="button" @click="fileOpen">파일찾기</v-btn>
    </div>

  </div>
</template>

<script>
 export default {
    data() {
      return {
        //체크박스
        checkboxDataVal: true,
        checkboxDataVal2: {
          type: [],
          check: false,
        },
        checkboxListDataVal:[],
        checkboxListData:[
          {value:'check1', label:'체크1'},
          {value:'check2', label:'체크2'},
          {value:'check3', label:'체크3'},
          {value:'check4', label:'체크4'},
        ],
        //라디오
        radioCheck:'1',
        optList1:[
          {value:'check1', label:'라디오1'},
          {value:'check2', label:'라디오2'}
        ],
        optsList2Checked:'',
        optList2:[
          {id:'id1', label:'라디오1'},
          {id:'id2', label:'라디오2'},
          {id:'id3', label:'라디오3'}
        ],
        //탭
        tabList:[
          {value:'tab1', label:'탭1'},
          {value:'tab2', label:'탭2'},
          {value:'tab3', label:'탭3'}
        ],

        //슬라이더
        sliderVal:10,

            ruleForm: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          check: false,
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        },
        //별점
        rateval:2,
        fileVal:'',        
        rules: {
          name: [
            { required: true, message: 'Please input Activity name', trigger: 'blur' },
            { min: 3, max: 5, message: 'Length should be 3 to 5', trigger: 'blur' }
          ],
          region: [
            { required: true, message: 'Please select Activity zone', trigger: 'change' }
          ],
          date1: [
            { type: 'date', required: true, message: 'Please pick a date', trigger: 'change' }
          ],
          date2: [
            { type: 'date', required: true, message: 'Please pick a time', trigger: 'change' }
          ],
          type: [
            { type: 'array', required: true, message: 'Please select at least one activity type', trigger: 'change' }
          ],
          type2: [
            { required: true, message: 'Please select at least one activity type', trigger: 'change' }
          ],
          resource: [
            { required: true, message: 'Please select activity resource', trigger: 'change' }
          ],
          desc: [
            { required: true, message: 'Please input activity form', trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      chanteSliderVal(){
        console.log(this.sliderVal);
      },
      changeFile(e) {
        var files = e.target.files || e.dataTransfer.files
        this.fileVal = files[0].name

        this.addPhotoFile(this.$refs.fileInput, function(src, size){
          
        });
      },
      fileDelete(){
        this.$refs.fileInput.value = ''
        this.fileVal = ''
      },
      fileOpen(){
        this.$refs.fileInput.click()
      },   

    addPhotoFile(obj, callback){
      let src, size

      if (obj.files && obj.files[0]) {
        var reader = new FileReader();
        reader.readAsDataURL(obj.files[0]);
        reader.onload = function (e) {
          size = obj.files[0].size
          src = e.target.result
          callback(src, size);
        }
      }
    }	

    },
    mounted(){
    }
  };
</script>

<style>

</style>
