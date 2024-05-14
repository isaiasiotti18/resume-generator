<template>
  <div class="experience-container">
    <h3>Experiência Profissional</h3>
    <div class="experience-item" v-for="(experience, index) in experiences" :key="index">
      <input class="form-control" v-model="experience.title" placeholder="Título" required/>
      <input class="form-control" v-model="experience.company" placeholder="Empresa" required/>
      <textarea class="form-control" v-model="experience.description" placeholder="Descrição" required></textarea>
      <button class="btn btn-danger" @click="removeExperience(index)">Remover</button>
    </div>
    <button type="button" @click="addExperience">Adicionar Experiência</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      experiences: [{ title: '', company: '', description: '' }]
    };
  },
  methods: {
    addExperience() {
      this.experiences.push({ title: '', company: '', description: '' });
    },
    removeExperience(index) {
      this.experiences.splice(index, 1);
    }
  },
  props: ['value'],
  watch: {
    experiences: {
      handler(newVal) {
        this.$emit('input', newVal);
      },
      deep: true
    }
  }
};
</script>

<style scoped>
.experience-container {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.experience-item {
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
