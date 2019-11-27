<template>
  <div id="view-employee">
    <h3>View Employee</h3>
  </div>
</template>

<script>
import db from './firebaseinit'
export default {
  name: 'view-employee',
  data() {
    return {
      employee_id: null,
      name: null,
      dept: null,
      position: null
    }
  },
  beforeRouteEnter (to, from, next) {
    db.collection('employees').where('employee_id','==',to.params.employee_id)
      .get().then(querySnapshot => {
        querySnapshot.forEach(doc => {
          next(vm => {
            vm.employee_id = doc.data().employee_id
            vm.name = doc.data().name
            vm.dept = doc.data().dept
            vm.position = doc.data().position
          })
        })
      })
  },
  watch() {
    ''
  }
}
</script>

<style>

</style>
