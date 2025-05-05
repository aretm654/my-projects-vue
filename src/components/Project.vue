<template>
    <div class="project-container">
      <a :href="link" target="_blank" rel="noopener noreferrer" class="project-link">
        <img :src="photo" :alt="text" class="project-image" />
      </a>
  
      <div class="project-text">
        <a :href="link" target="_blank" rel="noopener noreferrer" class="text-link">
          {{ link }} - {{ text }}
        </a>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Project',
    props: {
      link: {
        type: String,
        required: true,
      },
      photo: {
        type: String,
        required: true,
      },
      text: {
        type: String,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  .project-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: auto;
    max-width: 300px;
  }
  
  .project-link {
    display: block;
    transition: transform 0.3s ease;
  }
  
  .project-link:hover {
    transform: scale(1.05);
  }
  
  .project-image {
    width: 100%;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
  
  .project-text {
    margin-top: 10px;
    text-align: center;
    color: white;
    font-family: 'Arial', sans-serif;
    font-size: 16px;
  }
  
  .text-link {
    color: white;
    text-decoration: none;
    transition: color 0.3s ease;
  }
  
  .text-link:hover {
    color: #42b983;
  }
  </style>