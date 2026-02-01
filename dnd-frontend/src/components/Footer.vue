<template>
  <footer class="footer">
    <div class="footer-content">
      <p>&copy; {{ currentYear }} {{ companyName }}. Все права защищены.</p>
      <div class="footer-links">
        <a href="/privacy">Политика конфиденциальности</a>
        <a href="/terms">Условия использования</a>
        <a href="/contact">Контакты</a>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'TheFooter',
  props: {
    companyName: {
      type: String,
      default: 'Моя компания',
    },
  },
  data() {
    return {
      currentYear: new Date().getFullYear(),
    }
  },
}
</script>

<style scoped>
.footer {
  background-color: #f8f9fa;
  border-top: 1px solid #e2e8f0;
  padding: 1.25rem 1rem;
  margin-top: 2rem;
}

.footer-content {
  max-width: 720px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.875rem;
  color: #64748b;
}

.footer-links {
  display: flex;
  gap: 1rem;
}

.footer-links a {
  color: #475569;
  text-decoration: none;
  transition: color 0.15s ease;
}

.footer-links a:hover {
  color: #3b82f6;
}
</style>
