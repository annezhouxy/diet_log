<template>
  <div>
    <h1>This is Update view</h1>
    <div>
      <form novalidate class="md-layout" @submit.prevent="validateDietLog">
        <md-card class="md-layout-item md-size-50 md-small-size-100">
          <md-card-header>
            <div class="md-title">DietLog</div>
          </md-card-header>

          <md-card-content>
            <div class="md-layout md-gutter">
              <div class="md-layout-item md-small-size-100">
                <md-field>
                  <label for="date">Date</label>
                  <md-input
                    name="date"
                    id="date"
                    v-model="form.date"
                    :disabled="sending"
                  />
                  <span class="md-error" v-if="!$v.form.date.required"
                    >The date is required</span
                  >
                  <span class="md-error" v-else-if="!$v.form.date.minlength"
                    >Invalid date</span
                  >
                </md-field>
              </div>

              <div class="md-layout-item md-small-size-100">
                <md-field>
                  <label for="time">Time</label>
                  <md-input
                    name="time"
                    id="time"
                    v-model="form.time"
                    :disabled="sending"
                  />
                  <span class="md-error" v-if="!$v.form.time.required"
                    >The time is required</span
                  >
                  <span class="md-error" v-else-if="!$v.form.time.minlength"
                    >Invalid time</span
                  >
                </md-field>
              </div>
            </div>

            <div class="md-layout md-gutter">
              <div class="md-layout-item md-small-size-100">
                <md-field>
                  <label for="category">Category</label>
                  <md-select
                    name="category"
                    id="category"
                    v-model="form.category"
                    md-dense
                    :disabled="sending"
                  >
                    <md-option></md-option>
                    <md-option value="Vegetable">Vegetable</md-option>
                    <md-option value="Meat">Meat</md-option>
                    <md-option value="Dairy">Dairy</md-option>
                    <md-option value="Fruit">Fruit</md-option>
                    <md-option value="Grain">Grain</md-option>
                  </md-select>
                  <span class="md-error">The category is required</span>
                </md-field>
              </div>

              <div class="md-layout-item md-small-size-100">
                <md-field>
                  <label for="name">Name</label>
                  <md-input
                    name="name"
                    id="name"
                    v-model="form.name"
                    :disabled="sending"
                  />
                  <span class="md-error" v-if="!$v.form.name.required"
                    >The name is required</span
                  >
                  <span class="md-error" v-else-if="!$v.form.name.minlength"
                    >Invalid name</span
                  >
                </md-field>
              </div>

              <div class="md-layout-item md-small-size-100">
                <md-field>
                  <label for="weight">Weight</label>
                  <md-input
                    name="weight"
                    id="weight"
                    v-model="form.weight"
                    :disabled="sending"
                  />
                  <span class="md-error" v-if="!$v.form.weight.required"
                    >The weight is required</span
                  >
                  <span class="md-error" v-else-if="!$v.form.weight.minlength"
                    >Invalid weight</span
                  >
                </md-field>
              </div>

              <div class="md-layout-item md-small-size-100">
                <md-field>
                  <label for="calories">Calories</label>
                  <md-input
                    name="calories"
                    id="calories"
                    v-model="form.caleries"
                    :disabled="sending"
                  />
                  <span class="md-error" v-if="!$v.form.calories.required"
                    >The calories is required</span
                  >
                  <span class="md-error" v-else-if="!$v.form.calories.minlength"
                    >Invalid calories</span
                  >
                </md-field>
              </div>
            </div>
          </md-card-content>

          <md-progress-bar md-mode="indeterminate" v-if="sending" />

          <md-card-actions>
            <md-button
              type="submit"
              class="md-primary"
              :disabled="sending"
              @click="updateDietLog"
              >Update DietLog</md-button
            >
          </md-card-actions>
        </md-card>

        <md-snackbar :md-active.sync="dietLogSaved"
          >The DietLog {{ lastDietLog }} was saved with success!</md-snackbar
        >
      </form>
    </div>
  </div>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, minLength } from "vuelidate/lib/validators";

export default {
  name: "UpdateView",
  mixins: [validationMixin],
  data: () => ({
    form: {
      date: null,
      time: null,
      category: null,
      name: null,
      weight: null,
      caleries: null,
    },
    dietLogSaved: false,
    sending: false,
    lastDietLog: null,
  }),
  validations: {
    form: {
      date: {
        required,
        minLength: minLength(9),
      },
      time: {
        required,
        minLength: minLength(4),
      },
      category: {
        required,
      },
      name: {
        required,
        minLength: minLength(3),
      },
      weight: {
        required,
      },
      calories: {
        required,
      },
    },
  },
  methods: {
    updateDietLog() {
      this.form.id = parseInt(this.form.id);
      console.log(JSON.stringify(this.form));
      const serverURL = 
      process.env.NODE_ENV === "production"
      ? "https://3vkc0vullg.execute-api.us-east-2.amazonaws.com/dev"
      : "http://localhost:3000"
      fetch(serverURL+"/dietLog", {
      
        method: "PUT", // *GET, POST, PUT, DELETE, etc.
        mode: "cors", // no-cors, *cors, same-origin
        headers: {
          "Content-Type": "application/json",
          // "Access-Control-Allow-Origin": "*",
          Accept: "*/*",
        },
        body: JSON.stringify(this.form),
      })
        .then((dietLog) => {
          return dietLog.json();
        })
        .then((data) => {
          console.log(data);
        })
        .catch((err) => {
          console.log(err);
        });
    },

    getValidationClass(fieldName) {
      const field = this.$v.form[fieldName];

      if (field) {
        return {
          "md-invalid": field.$invalid && field.$dirty,
        };
      }
    },
    clearForm() {
      this.$v.$reset();
      this.form.date = null;
      this.form.time = null;
      this.form.category = null;
      this.form.name = null;
      this.form.weight = null;
      this.form.caleries = null;
    },
    saveDietLog() {
      this.sending = true;

      // Instead of this timeout, here you can call your API
      window.setTimeout(() => {
        this.lastDietLog = `${this.form.date} ${this.form.time}`;
        this.dietLogSaved = true;
        this.sending = false;
        console.log(this.form);
        this.clearForm();
      }, 1500);
    },
    validateDietLog() {
      console.log(this.form);
      this.$v.$touch();

      if (!this.$v.$invalid) {
        this.saveDietLog();
      }
    },
  },
};
</script>