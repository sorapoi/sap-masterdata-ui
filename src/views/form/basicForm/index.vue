<!-- #     'applyTypes': '申请类型',
    #     'materialType': '物料类型',
    #     'projectOrBusiness': '项目或商业化',
    #     'factory': '5000',
    #     'isQuality': '是否维护质量视图',
    #     'qualityDepartment': '质量部门',
    #     'isFeed': '进料加工',
    #     'isBatch': '批次管理',
    #     'commonName': '通用名',
    #     'englishName': '英文名称',
    #     'materialGroup': '110101',
    #     'standard': '规格',
    #     'remark': '备注',
    #     'manufacturerName': '生产厂家名称',
    #     'manufacturerMaterialName': '厂家物料名称',
    #     'market': '市场',
    #     'guideline': '参考标准',
    #     'internalControlStandards': '内控标准',
    #     'describe': '描述',
    #     'basicUnit': '基本单位',
    #     'applicant': '申请人' 
        # 'packagingSpecifications': '包装规格',
        # 'RAUBE': '温度',
        # 'MHDRZ': '最小剩余货架寿命',
        # 'MHDHB': '总货架寿命',
        # 'IPRKZ': 'SLED的期间标识',
        # 'RDMHD': 'SLED舍入规则',
        # 'sheetType': '片型',
        # 'packageStyle': '包装形式',
        # 'MinimumPackageSize': '最小包装规格',
        # 'MinimumPackageSizeUnit': '最小包装规格单位',
        # 'MediumPackageSize': '中包装规格',
        # 'MediumPackageSizeUnit': '中包装规格单位',
        # 'MaximumPackageSize': '最大包装规格',
        # 'MaximumPackageSizeUnit': '最大包装规格单位',}
-->
<template>
  <div>
    <div class="n-layout-page-header">
      <n-card :bordered="false" title="SAP物料主数据新增">SAP物料主数据新增。</n-card>
    </div>
    <n-card :bordered="false" class="mt-4 proCard">
      <n-form
        :label-width="100"
        :model="formValue"
        :rules="rules"
        label-placement="left"
        ref="formRef"
        class="py-8"
      >
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="2">
            <n-form-item path="applyTypes">
              <n-select
                :options="applyTypes"
                v-model:value="formValue.applyTypes"
                style="padding-left: 20px"
              />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="2">
            <n-form-item>
              <n-select
                :options="materialType"
                v-model:value="formValue.materialType"
                style="padding-left: 20px"
              />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="2">
            <n-form-item>
              <n-select
                :options="projectOrBusiness"
                v-model:value="formValue.projectOrBusiness"
                style="padding-left: 20px"
              />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="2">
            <n-form-item label="工厂：">
              <n-select :options="factory" v-model:value="formValue.factory" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="3">
            <n-form-item label="检验部门：">
              <n-select :options="qualityDepartment" v-model:value="formValue.qualityDepartment" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="3">
            <n-form-item label="维护质量视图：" style="padding-left: 20px">
              <n-radio-group v-model:value="formValue.isQuality" name="isQuality">
                <n-space>
                  <n-radio :value="1">是</n-radio>
                  <n-radio :value="2">否</n-radio>
                </n-space>
              </n-radio-group>
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="2">
            <n-form-item label="申请人：">
              <n-input v-model:value="formValue.applicant" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="8">
            <n-form-item label="通用名：" path="commonName">
              <n-input
                v-model:value="formValue.commonName"
                placeholder="请输入通用名"
                maxlength="32"
                show-count
              />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="8">
            <n-form-item label="英文名称：">
              <n-input v-model:value="formValue.englishName" @input="checkLetter" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="2">
            <n-form-item label="基本计量单位：">
              <n-input v-model:value="formValue.basicUnit" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="3">
            <n-form-item label="进料加工：" style="padding-left: 20px">
              <n-radio-group v-model:value="formValue.isFeed" name="isFeed">
                <n-space>
                  <n-radio :value="1">是</n-radio>
                  <n-radio :value="2">否</n-radio>
                  <n-radio :value="3">NA</n-radio>
                </n-space>
              </n-radio-group>
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="4">
            <n-form-item label="批次管理：" style="padding-left: 20px">
              <n-radio-group v-model:value="formValue.isBatch" name="isBatch">
                <n-space>
                  <n-radio :value="1">是</n-radio>
                  <n-radio :value="2">否</n-radio>
                </n-space>
              </n-radio-group>
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="3">
            <n-form-item label="物料组：" path="materialGroup">
              <n-input v-model:value="formValue.materialGroup" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="5">
            <n-form-item label="规格：" style="padding-left: 20px" path="standard">
              <n-input v-model:value="formValue.standard" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="8">
            <n-form-item label="生产厂家名称：">
              <n-input v-model:value="formValue.manufacturerName" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="8">
            <n-form-item label="厂家物料名称：">
              <n-input v-model:value="formValue.manufacturerMaterialName" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="2">
            <n-form-item label="市场：">
              <n-input v-model:value="formValue.market" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="3">
            <n-form-item label="参考标准：" style="padding-left: 20px">
              <n-input v-model:value="formValue.guideline" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="3">
            <n-form-item label="内控标准：" style="padding-left: 20px">
              <n-input v-model:value="formValue.internalControlStandards" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item
            offset="1"
            span="2"
            v-if="formValue.materialType === 3 || formValue.materialType === 4"
          >
            <n-form-item label="片型：">
              <n-input v-model:value="formValue.sheetType" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="3" v-if="formValue.materialType === 4">
            <n-form-item label="包装形式：" style="padding-left: 20px">
              <n-input v-model:value="formValue.packageStyle" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="3" v-if="formValue.materialType === 4">
            <n-form-item label="包装规格：" style="padding-left: 20px">
              <n-input v-model:value="formValue.packagingSpecifications" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen" v-if="formValue.materialType === 4">
          <n-grid-item offset="1" span="2">
            <n-form-item label="温度：">
              <n-input v-model:value="formValue.RAUBE" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="2">
            <n-form-item label="最小货架寿命：" style="padding-left: 20px">
              <n-input v-model:value="formValue.MHDRZ" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="2">
            <n-form-item label="总货架寿命：" style="padding-left: 20px">
              <n-input v-model:value="formValue.MHDHB" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen" v-if="formValue.materialType === 4">
          <n-grid-item offset="1" span="2">
            <n-form-item label="期间标识：">
              <n-input v-model:value="formValue.IPRKZ" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="2">
            <n-form-item label="舍入规则：" style="padding-left: 20px">
              <n-input v-model:value="formValue.RDMHD" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen" v-if="formValue.materialType === 4">
          <n-grid-item offset="1" span="2">
            <n-form-item label="最小包装规格：">
              <n-input v-model:value="formValue.MinimumPackageSize" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="3">
            <n-form-item label="最小包装单位：" style="padding-left: 20px">
              <n-input v-model:value="formValue.MinimumPackageSizeUnit" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen" v-if="formValue.materialType === 4">
          <n-grid-item offset="1" span="2">
            <n-form-item label="中包装规格：">
              <n-input v-model:value="formValue.MediumPackageSize" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="3">
            <n-form-item label="中包装单位：" style="padding-left: 20px">
              <n-input v-model:value="formValue.MediumPackageSizeUnit" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen" v-if="formValue.materialType === 4">
          <n-grid-item offset="1" span="2">
            <n-form-item label="最大包装规格：">
              <n-input v-model:value="formValue.MaximumPackageSize" />
            </n-form-item>
          </n-grid-item>
          <n-grid-item span="3">
            <n-form-item label="最大包装单位：" style="padding-left: 20px">
              <n-input v-model:value="formValue.MaximumPackageSizeUnit" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="8">
            <n-form-item label="备注：">
              <n-input v-model:value="formValue.remark" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="1" span="8">
            <n-form-item label="描述：">
              <n-input type="textarea" v-model:value="formValue.describe" />
            </n-form-item>
          </n-grid-item>
        </n-grid>
        <n-grid cols="12" responsive="screen">
          <n-grid-item offset="7" span="3">
            <n-space>
              <n-button type="primary" @click="formSubmit">提交</n-button>
              <n-button @click="resetForm">重置</n-button>
            </n-space>
          </n-grid-item>
        </n-grid>
      </n-form>
    </n-card>
  </div>
</template>

<script lang="ts" setup>
  import { ref, unref, reactive } from 'vue';
  import { useMessage } from 'naive-ui';
  // import { useGlobSetting } from '@/hooks/setting';
  import axios from 'axios';
  //import { func } from 'vue-types';
  // import { createDecipheriv } from 'crypto';

  // const globSetting = useGlobSetting();

  const applyTypes = [
    {
      label: '新增',
      value: 1,
    },
    {
      label: '修改',
      value: 2,
    },
    {
      label: '删除',
      value: 3,
    },
  ];

  const materialType = [
    {
      label: '原辅料',
      value: 1,
    },
    {
      label: '包材',
      value: 2,
    },
    {
      label: '半成品',
      value: 3,
    },
    {
      label: '成品',
      value: 4,
    },
  ];

  const projectOrBusiness = [
    {
      label: '研发',
      value: 1,
    },
    {
      label: '商业化',
      value: 2,
    },
  ];

  const factory = [
    {
      label: '5000',
      value: 5000,
    },
    {
      label: '8000',
      value: 8000,
    },
  ];

  const qualityDepartment = [
    {
      label: '制剂分析中心',
      value: 1,
    },
    {
      label: '制剂项目一部',
      value: 2,
    },
    {
      label: '制剂项目二部',
      value: 3,
    },
  ];

  const rules = {
    commonName: {
      required: true,
      message: '请输入物料通用名',
      trigger: 'blur',
    },
    materialGroup: {
      required: true,
      message: '请输入物料物料组',
      trigger: 'blur',
    },
    standard: {
      required: true,
      message: '请输入物料规格',
      trigger: 'blur',
    },
  };

  const formRef: any = ref(null);
  const message = useMessage();

  const defaultValueRef = () => ({
    applyTypes: 1,
    materialType: 1,
    projectOrBusiness: 1,
    factory: 5000,
    isQuality: 1,
    qualityDepartment: 1,
    isFeed: 3,
    isBatch: 1,
    commonName: '',
    englishName: '',
    materialGroup: '',
    standard: '',
    remark: '',
    manufacturerName: '',
    manufacturerMaterialName: '',
    market: '',
    guideline: '',
    internalControlStandards: '',
    describe: '',
    basicUnit: '',
    applicant: '',
    sheetType: '',
    packageStyle: '',
    packagingSpecifications: '',
    RAUBE: '',
    MHDRZ: '',
    MHDHB: '',
    IPRKZ: '',
    RDMHD: '',
    MinimumPackageSize: '',
    MinimumPackageSizeUnit: '',
    MediumPackageSize: '',
    MediumPackageSizeUnit: '',
    MaximumPackageSize: '',
    MaximumPackageSizeUnit: '',
  });

  let formValue = reactive(defaultValueRef());

  function checkLetter(str: string) {
    formValue.englishName = str.replace(/[0-9]+/g, '');
  }

  function formSubmit() {
    formRef.value.validate((errors) => {
      if (!errors) {
        // axios.post('/api/form', formValue).then(function(response) {
        //   window.open('api/download/' + response.data['docname'], '_blank');
        //   window.open('api/download/' + response.data['excelName'], '_blank');
        // });
        alert(JSON.stringify(formValue));
      } else {
        message.error('验证失败，请填写完整信息');
      }
    });
  }

  function resetForm() {
    formRef.value.restoreValidation();
    formValue = Object.assign(unref(formValue), defaultValueRef());
  }
</script>
