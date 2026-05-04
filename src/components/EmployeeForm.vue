<template>
  <div class="card bg-dark text-light shadow-lg mb-4 border-0">
    <div class="card-body">
      <form @submit.prevent="submitForm">
        <div class="row g-3">
          <div class="col-md-2">
            <input v-model="localEmployee.employeeId" class="form-control bg-secondary text-light border-0" placeholder="Emp ID" required />
          </div>
          <div class="col-md-2">
            <input v-model="localEmployee.name" class="form-control bg-secondary text-light border-0" placeholder="Name" required />
          </div>
          <div class="col-md-2">
            <input v-model="localEmployee.designation" class="form-control bg-secondary text-light border-0" placeholder="Designation" required />
          </div>
          <div class="col-md-2">
            <input v-model="localEmployee.department" class="form-control bg-secondary text-light border-0" placeholder="Department" required />
          </div>
          <div class="col-md-2">
            <input v-model.number="localEmployee.salary" type="number" class="form-control bg-secondary text-light border-0" placeholder="Salary" required />
          </div>
          <div class="col-md-2">
            <button class="btn btn-success w-100 fw-bold">
              {{ isEdit ? 'Update' : 'Add' }}
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: ["employee", "isEdit"],
  emits: ["save"],

  data() {
    return {
      localEmployee: { ...this.employee }
    };
  },

  watch: {
    employee: {
      handler(newVal) {
        this.localEmployee = { ...newVal };
      },
      deep: true
    }
  },

  methods: {
    submitForm() {
      this.$emit("save", { ...this.localEmployee });
      this.localEmployee = {
        employeeId: "",
        name: "",
        designation: "",
        department: "",
        salary: ""
      };
    }
  }
};
</script>