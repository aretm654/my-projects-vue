<template>
    <header class="header">
      <div class="header__content">
        <div class="header__logo">
          <img 
            src="https://static.tildacdn.com/tild3064-6338-4337-b261-623761363462/999966666.png" 
            alt="Matrix Logo"
            class="logo"
          >
        </div>
        <span class="header__name">Artem Gorodeckiy</span>
      </div>
    </header>
  </template>
  
  <script>
  export default {
    name: 'MatrixHeader'
  }
  </script>
  
  <style scoped>
  .header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background: rgba(0, 0, 0, 0.9);
    padding: 12px 20px;
    z-index: 1000;
    font-family: 'Courier New', monospace;
    box-shadow: 0 4px 30px rgba(0, 255, 65, 0.4);
    border-bottom: 1px solid rgba(0, 255, 65, 0.2);
    backdrop-filter: blur(5px);
  }
  
  .header__content {
    display: flex;
    align-items: center;
    margin: 0 auto;
  }
  
  .header__logo {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    overflow: hidden;
    margin-right: 15px;
    border: 1px solid #00ff41;
    box-shadow: 0 0 15px rgba(0, 255, 65, 0.5);
    transition: all 0.3s ease;
  }
  
  .header__logo:hover {
    transform: scale(1.05);
    box-shadow: 0 0 25px rgba(0, 255, 65, 0.8);
  }
  
  .logo {
    width: 100%;
    height: 100%;
    object-fit: cover;
    filter: sepia(100%) hue-rotate(60deg) saturate(500%);
  }
  
  .header__name {
    color: #00ff41;
    font-size: 1.5rem;
    font-weight: bold;
    text-shadow: 0 0 8px #00ff41;
    letter-spacing: 2px;
    animation: flicker 3s infinite;
  }
  @keyframes flicker {
    0%, 19%, 21%, 23%, 25%, 54%, 56%, 100% {
      opacity: 1;
      text-shadow: 0 0 8px #00ff41;
    }
    20%, 22%, 24%, 55% {
      opacity: 0.7;
      text-shadow: 0 0 2px #00ff41;
    }
  }
  
  @media (max-width: 768px) {
    .header {
      padding: 8px 15px;
    }
    .header__name {
      font-size: 1.2rem;
    }
  }
  </style>