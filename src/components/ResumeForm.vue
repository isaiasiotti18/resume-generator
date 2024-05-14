<template>
  <div class="container">
    <h2>Gerar Currículo</h2>
    <form class="resume-form" @submit.prevent="generateResume">
      <div class="form-group">
        <label>Nome:</label>
        <input class="form-control" v-model="resume.name" type="text" placeholder="Nome" required />
      </div>
      <div class="form-group">
        <label>Email: </label>
        <input class="form-control" v-model="resume.contact" type="email" placeholder="Email" required />    
      </div>

      <div class="form-group">
        <label>Celular/Whatsapp: </label>
        <input class="form-control" v-model="resume.phone" type="text" placeholder="(99) 99999-9999" required />    
      </div>

      <div class="form-group">
        <label>Github: </label>
        <input class="form-control" v-model="resume.github" type="text" placeholder="https://github.com/username" required />    
      </div>
      
      <div class="form-group">
        <label>Linkedin: </label>
        <input class="form-control" v-model="resume.linkedin" type="text" placeholder="https://linkedin.com/in/username" required />    
      </div>        

      <div class="form-group">
        <label for="description">Resumo</label>
        <textarea class="form-control" v-model="resume.description" placeholder="Descrição" required></textarea>
      </div>
      <ExperienceForm v-model="resume.experience" />
      <EducationForm v-model="resume.education" />
      <button class="btn btn-primary" type="submit">Gerar Currículo</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';
import ExperienceForm from '@/components/ExperienceForm.vue';
import EducationForm from '@/components/EducationForm.vue';

export default {
  components: {
    ExperienceForm,
    EducationForm
  },
  data() {
    return {
      resume: {
        name: '',
        contact: '',
        phone: '',
        description: '',
        github: '',
        linkedin: '',
        experience: [],
        education: []
      }
    };
  },
  methods: {
    async generateResume() {
      try {
        const response = await axios.post('http://localhost:8000/api/v1/resume/generate_resume', this.resume);
        alert(`Currículo gerado com sucesso! Baixe em: ${response.data.file_path}`);
      } catch (error) {
        console.error(error);
        alert('Erro ao gerar currículo');
      }
    },
    addExperience() {
      this.resume.experience.push({ title: '', company: '', description: '' });
    },
    addEducation() {
      this.resume.education.push({ degree: '', institution: '', description: '' });
    }
  }
};
</script>

<style scoped>

label {
  margin-top: 5px;
  margin-bottom: 5px;
}
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.resume-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-control {
  padding: 10px;
  font-size: 16px;
  margin-top: 5px;
}

.btn {
  padding: 10px 15px;
  margin-top: 10px;
  font-size: 16px;
}

.btn-primary {
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

.btn-secondary {
  background-color: #6c757d;
  color: white;
  border: none;
  cursor: pointer;
}

.btn-primary:hover, .btn-secondary:hover {
  opacity: 0.8;
}

/* Responsividade */
@media (max-width: 600px) {
  .container {
    padding: 10px;
  }

  .form-control, .btn {
    width: 100%;
    box-sizing: border-box;
  }
}
</style>
