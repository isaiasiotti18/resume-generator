<template>
  <div class="education-container">
    <h3>Formação Acadêmica</h3>
    <div v-for="(education, index) in educations" :key="index">
      <input class="form-control" v-model="education.degree" placeholder="Grau" required />
      <input class="form-control" v-model="education.institution" placeholder="Instituição" required />
      <textarea class="form-control" v-model="education.description" placeholder="Descrição" required></textarea>
      <button class="btn btn-danger" @click="removeEducation(index)">Remover</button>
    </div>
    <button type="button" @click="addEducation">Adicionar Formação</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      educations: [{ degree: '', institution: '', description: '' }]
    };
  },
  methods: {
    addEducation() {
      this.educations.push({ degree: '', institution: '', description: '' });
    },
    removeEducation(index) {
      this.educations.splice(index, 1);
    }
  },
  props: ['value'],
  watch: {
    educations: {
      handler(newVal) {
        this.$emit('input', newVal);
      },
      deep: true
    }
  }
};
</script>

<style scoped>
.education-container {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.education-item {
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
}

.form-control {
  padding: 10px;
  font-size: 16px;
  margin-top: 5px;
  width: 100%;
  box-sizing: border-box;
}

.btn {
  padding: 10px 15px;
  font-size: 16px;
  margin-top: 10px;
}

.btn-danger {
  background-color: #dc3545;
  color: white;
  border: none;
  cursor: pointer;
}

.btn-danger:hover {
  opacity: 0.8;
}
</style>