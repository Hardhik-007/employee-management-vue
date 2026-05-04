<template>
  <div class="app-bg min-vh-100 py-4">
    <div class="container">
      <h2 class="text-center text-light mb-4 fw-bold">
        Employee Management System
      </h2>

      <EmployeeForm
        :employee="employee"
        :isEdit="editMode"
        @save="handleSave"
      />

      <EmployeeTable
        :employees="employees"
        @edit="handleEdit"
        @delete="handleDelete"
      />
    </div>
  </div>
</template>

<script>
import EmployeeForm from "./components/EmployeeForm.vue";
import EmployeeTable from "./components/EmployeeTable.vue";
import api from "./services/api";

export default {
  components: { EmployeeForm, EmployeeTable },

  data() {
    return {
      employees: [],
      employee: {
        employeeId: "",
        name: "",
        designation: "",
        department: "",
        salary: ""
      },
      editMode: false,
      editId: null
    };
  },

  methods: {
    async fetchEmployees() {
      const res = await api.getEmployees();
      this.employees = res.data;
    },

    async handleSave(emp) {
      if (this.editMode) {
        await api.updateEmployee(this.editId, emp);
        this.editMode = false;
        this.editId = null;
      } else {
        await api.addEmployee(emp);
      }
      this.resetForm();
      this.fetchEmployees();
    },

    handleEdit(emp) {
      this.employee = { ...emp };
      this.editMode = true;
      this.editId = emp.id;
    },

    async handleDelete(id) {
      await api.deleteEmployee(id);
      this.fetchEmployees();
    },

    resetForm() {
      this.employee = {
        employeeId: "",
        name: "",
        designation: "",
        department: "",
        salary: ""
      };
    }
  },

  mounted() {
    this.fetchEmployees();
  }
};
</script>

<style>
.app-bg {
  background: linear-gradient(135deg, #0f172a, #1e293b);
}
</style>