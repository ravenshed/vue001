<template>
  <div class="container">
    <h1>Job Application Dashboard</h1>

    <!-- Tabs -->
    <div class="tabs">
      <button @click="currentTab = 'form'">
        Applicant Form
      </button>

      <button @click="currentTab = 'dashboard'">
        Administrator Dashboard
      </button>
    </div>

    <!-- Applicant Form -->
    <div v-if="currentTab === 'form'" class="form-section">
      <h2>Applicant Form</h2>

      <form @submit.prevent="submitApplication">

        <!-- Firstname -->
        <div>
          <label>Firstname</label>
          <input
            type="text"
            v-model="applicant.firstname"
            required
          />
        </div>

        <!-- Surname -->
        <div>
          <label>Surname</label>
          <input
            type="text"
            v-model="applicant.surname"
            required
          />
        </div>

        <!-- DOB -->
        <div>
          <label>Date of Birth</label>
          <input
            type="date"
            v-model="applicant.dob"
            required
          />
        </div>

        <!-- Address -->
        <div>
          <label>Address</label>
          <textarea
            v-model="applicant.address"
            required
          ></textarea>
        </div>

        <!-- Phone -->
        <div>
          <label>Phone Number</label>
          <input
            type="tel"
            v-model="applicant.phone"
            required
          />
        </div>

        <!-- Gender -->
        <div>
          <label>Gender</label>

          <label>
            <input
              type="radio"
              value="Male"
              v-model="applicant.gender"
            />
            Male
          </label>

          <label>
            <input
              type="radio"
              value="Female"
              v-model="applicant.gender"
            />
            Female
          </label>

          <label>
            <input
              type="radio"
              value="Other"
              v-model="applicant.gender"
            />
            Other
          </label>
        </div>

        <!-- National ID -->
        <div>
          <label>National ID</label>
          <input
            type="text"
            v-model="applicant.nationalId"
            required
          />
        </div>

        <!-- Submit -->
        <button type="submit">
          Submit Application
        </button>

      </form>

      <!-- Success Message -->
      <p v-if="successMessage" class="success">
        {{ successMessage }}
      </p>
    </div>

    <!-- Administrator Dashboard -->
    <div v-if="currentTab === 'dashboard'" class="dashboard">
      <h2>Administrator Dashboard</h2>

      <!-- No Applicants -->
      <p v-if="applications.length === 0">
        No applicants yet.
      </p>

      <!-- Table -->
      <table v-else border="1" cellpadding="10">
        <thead>
          <tr>
            <th>Firstname</th>
            <th>Surname</th>
            <th>DOB</th>
            <th>Address</th>
            <th>Phone</th>
            <th>Gender</th>
            <th>National ID</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="(app, index) in applications" :key="index">
            <td>{{ app.firstname }}</td>
            <td>{{ app.surname }}</td>
            <td>{{ app.dob }}</td>
            <td>{{ app.address }}</td>
            <td>{{ app.phone }}</td>
            <td>{{ app.gender }}</td>
            <td>{{ app.nationalId }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

// Current Tab
const currentTab = ref("form");

// Success Message
const successMessage = ref("");

// Applications Array
const applications = ref([]);

// Applicant Object
const applicant = ref({
  firstname: "",
  surname: "",
  dob: "",
  address: "",
  phone: "",
  gender: "",
  nationalId: "",
});

// Submit Function
const submitApplication = () => {

  // Save applicant
  applications.value.push({
    ...applicant.value
  });

  // Success message
  successMessage.value = "Application submitted successfully!";

  // Clear form
  applicant.value = {
    firstname: "",
    surname: "",
    dob: "",
    address: "",
    phone: "",
    gender: "",
    nationalId: "",
  };
};
</script>

<style>
.container {
  max-width: 800px;
  margin: auto;
  font-family: Arial;
}

.tabs {
  margin-bottom: 20px;
}

button {
  margin-right: 10px;
  padding: 10px;
}

form div {
  margin-bottom: 15px;
}

input,
textarea {
  width: 100%;
  padding: 8px;
}

.success {
  color: rgb(199, 70, 102);
  margin-top: 15px;
}

table {
  width: 100%;
  border-collapse: collapse;
}
</style>