<template>
  <div class="about">
    <p>
      This project was created by
      <a href="https://github.com/tuthanhh" target="_blank" rel="noopener noreferrer"> tuthanhh </a>
    </p>
    <p>a way to prepare for <strong>CS300 - Software Engineering</strong>.</p>
    <p>It all started on 2/11/2025,</p>
    <p>with the goal of exploring and strengthening software engineering knowledge.</p>
  </div>
</template>

<style scoped>
.about {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  font-size: 1.2rem;
  padding: 20px;
  text-align: center;
  gap: 12px;
  color: #333;
  line-height: 1.6; /* smoother reading */
}

.about a {
  color: #007bff;
  text-decoration: none;
  margin-left: 4px;
}

.about a:hover {
  text-decoration: underline;
}
</style>
