<template>
  <div class="card bg-dark text-light shadow-lg border-0">
    <div class="card-body">
      <table class="table table-dark table-hover align-middle">
        <thead>
          <tr>
            <th>Emp ID</th>
            <th>Name</th>
            <th>Designation</th>
            <th>Department</th>
            <th>Salary</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="emp in employees" :key="emp.id">
            <td>{{ emp.employeeId }}</td>
            <td>{{ emp.name }}</td>
            <td>{{ emp.designation }}</td>
            <td>{{ emp.department }}</td>
            <td>₹ {{ emp.salary }}</td>
            <td>
              <button class="btn btn-outline-warning btn-sm me-2" @click="$emit('edit', emp)">
                Edit
              </button>
              <button class="btn btn-outline-danger btn-sm" @click="$emit('delete', emp.id)">
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: ["employees"]
};
</script>