# เปลี่ยนข้อความในฟอร์เป็นภาษาไทย
<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input
        filled
        v-model="name"
        label="ชื่อ-สกุล *"
        hint="ชื่อและนามสกุล"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาพิมพ์ชื่อ']"
      />

      <q-input
        filled
        type="number"
        v-model="age"
        label="อายุ *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'กรุณาใส่อายุ',
          val => val > 0 && val < 100 || 'กรุณาใส่อายุจริง'
        ]"
      />

      <q-toggle v-model="accept" label="ยอมรับ" />

      <div>
        <q-btn label="ยอมรับ" type="submit" color="primary"/>
        <q-btn label="ยกเลิก" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()

    const name = ref(null)
    const age = ref(null)
    const accept = ref(false)
    return {
      name,
      age,
      accept,
      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'You need to accept the license and terms first'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
      },
      onReset () {
        name.value = null
        age.value = null
        accept.value = false
      }
    }
  }
}
</script>
