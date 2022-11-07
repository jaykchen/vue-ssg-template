<template>
  <el-form :model="data" ref="formRef" :rules="rules">
    <el-form-item label="Name">
      <el-input type="text" v-model="data.name" placeholder="Enter your name" />
    </el-form-item>
    <el-form-item label="Email">
      <el-input type="text" v-model="data.email" placeholder="Enter your Email" />
    </el-form-item>
    <el-form-item label="Age" prop="age">
      <el-input type="text" v-model="data.age" placeholder="Age" />
    </el-form-item>
    <el-form-item label="Which option best describes your current role?">

      <el-select v-model="data.role" placeholder="please select your category">
        <el-option v-for="item in roleOptions" :key="item" :label="item" :value="item" />

      </el-select>
    </el-form-item>
    <el-form-item label="Would you recommend freeCodeCamp to a friend?">
      <el-radio-group v-model="data.recommend">
        <el-radio v-for="item in recommendOptions" :value="item.value" :label="item.label" :key="item.label">
          {{
              item.label
          }}
        </el-radio>

      </el-radio-group>

    </el-form-item>
    <el-form-item label="What is your favorite feature of freeCodeCamp?">
      <el-select v-model="data.feature" required placeholder="Please select a feature">
        <el-option v-for="option in featureOptions" :label="option" :key="option" />
      </el-select>
    </el-form-item>

    <el-form-item label="What would you like to see improved? (Check all that apply)">
      <el-checkbox-group v-model="data.improvements" :min="2" :max="5">
        <el-checkbox v-for="option in improveOptions" :label="option" :key="option">{{ option }}
        </el-checkbox>

      </el-checkbox-group>
    </el-form-item>

    <el-form-item label="Any comments or suggestions?">
      <el-input v-model="data.suggestions" type="textarea" placeholder="Enter your comments here..." />
    </el-form-item>



    <el-button style="confirm">Submit</el-button>
  </el-form>



</template>

<script setup lang="ts">
import { ref } from 'vue'
import 'element-plus/dist/index.css'
import type { FormRules, FormInstance } from 'element-plus'

const formRef = ref<FormInstance>()

const data = ref({
  name: '',
  email: '',
  age: '',
  role: '',
  recommend: 1,
  feature: '',
  improvements: [],
  suggestions: '',
})

const rules = ref<FormRules>({
  age: [{
    required: true,
    type: 'string',
  },
  {
    min: 1,
    max: 3,
    message: 'data out of range',
    trigger: 'change'
  }],
  improvements: [{
    required: true,
    type: 'array',
    message: 'please check a minimum of 2, and a max of 5',
    trigger: 'change'
  },
  {
    min: 2,
    max: 5,
    trigger: 'submit'
  }]
})

const recommendOptions = [
  { label: "Definitely", value: 1 },
  { label: "Maybe", value: 2 },
  { label: "Not sure", value: 3 },
]


const roleOptions = ['Student', 'Full-time Job', 'Full-time learner', 'Prefer not to say', 'Other']

const featureOptions = ['Challenge', 'Feature', 'Community', 'Open Source']

const improveOptions = [
  'Front-end Projects',
  'Back-end Projects',
  'Data Visualization',
  'Challenges',
  'Open Source Community',
  'Gitter help rooms',
  'Videos',
  'City Meetups',
  'Wiki',
  'Forum',
  'Additional Coursest',
]
</script>