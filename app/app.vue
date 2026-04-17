<template>
  <div class="app-shell">
    <div class="binary-grid">
      <span>01010101</span>
      <span>10101010</span>
      <span>00110011</span>
      <span>11001100</span>
      <span>01100110</span>
      <span>10011001</span>
    </div>

    <div class="hero-panel">
      <div class="hero-copy">
        <span class="eyebrow">QR Code Matrix</span>
        <h1>Blue QR codes with a binary glow</h1>
        <p class="hero-text">
          Type text or a URL, choose a style, and watch your code appear in a digital blue matrix.
        </p>

        <div class="controls">
          <label class="field">
            <span>Text or URL</span>
            <UInput v-model="text" placeholder="https://example.com" />
          </label>

          <label class="field">
            <span>Variant style</span>
            <USelect v-model="variant" :items="variants" />
          </label>
        </div>
      </div>

      <div class="preview-card">
        <div class="preview-badge">Live preview</div>
        <img class="qr-preview" width="320" :src="qr" alt="QR Code" />
        <p class="preview-note">Cool blue glass, glowing digits, and crisp digital contrast.</p>
      </div>
    </div>

    <div class="feature-strip">
      <div class="feature-item">
        <strong>Binary mood</strong>
        <span>Subtle ones and zeros float in the background for a tech-inspired feel.</span>
      </div>
      <div class="feature-item">
        <strong>Neon blue</strong>
        <span>Bright blue gradients and glassy cards create a futuristic style.</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { SVGVariant } from "nuxt-qrcode";

const text = ref("Hello World");
const variant = ref<SVGVariant>("dots");
const variants = ref(["default", "circle", "pixelated", "rounded", "dots"]);

const qr = useQrcode(text, {
  toBase64: true,
  variant: {
    inner: "dots",
    marker: "rounded",
    pixel: "rounded",
  },
  radius: 1,
  blackColor: "currentColor",
  whiteColor: "#ffff",
});
</script>

<style scoped>
.app-shell {
  position: relative;
  min-height: 100vh;
  padding: 3rem 1.5rem 2rem;
  color: #cce7ff;
  background: radial-gradient(circle at top left, rgba(96, 165, 250, 0.18), transparent 20%),
    radial-gradient(circle at bottom right, rgba(59, 130, 246, 0.16), transparent 25%),
    linear-gradient(180deg, #04172d 0%, #061f3d 42%, #0a294e 100%);
  display: flex;
  flex-direction: column;
  gap: 2rem;
  overflow: hidden;
}

.binary-grid {
  position: absolute;
  inset: 0;
  display: grid;
  grid-template-columns: repeat(6, minmax(0, 1fr));
  grid-template-rows: repeat(6, minmax(0, 1fr));
  gap: 2rem;
  padding: 2rem;
  pointer-events: none;
  opacity: 0.14;
}

.binary-grid span {
  align-self: center;
  justify-self: center;
  color: #7dd3fc;
  letter-spacing: 0.3em;
  font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
  font-size: 0.85rem;
  text-transform: uppercase;
}

.hero-panel {
  position: relative;
  width: min(1200px, 100%);
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1.2fr 0.9fr;
  gap: 2rem;
  align-items: center;
}

.hero-panel::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: 2.5rem;
  background: rgba(59, 130, 246, 0.18);
  filter: blur(20px);
  pointer-events: none;
}

.hero-copy {
  position: relative;
  padding: 2.4rem;
  border-radius: 2.25rem;
  background: rgba(7, 24, 45, 0.88);
  border: 1px solid rgba(96, 165, 250, 0.22);
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.24);
}

.eyebrow {
  display: inline-flex;
  margin-bottom: 1rem;
  padding: 0.55rem 0.95rem;
  border-radius: 999px;
  background: rgba(59, 130, 246, 0.88);
  color: #dbeafe;
  text-transform: uppercase;
  letter-spacing: 0.16em;
  font-size: 0.78rem;
  font-weight: 700;
}

.hero-copy h1 {
  margin: 0.75rem 0 1rem;
  font-size: clamp(2.5rem, 4vw, 3.8rem);
  line-height: 1.05;
  color: #bfdbfe;
}

.hero-text {
  max-width: 44rem;
  margin-bottom: 2rem;
  color: #c7d2fe;
  line-height: 1.85;
}

.controls {
  display: grid;
  gap: 1.25rem;
}

.field {
  display: grid;
  gap: 0.75rem;
  font-size: 0.95rem;
  color: #bfdbfe;
}

.field span {
  font-weight: 700;
}

.preview-card {
  position: relative;
  padding: 2rem;
  border-radius: 2rem;
  background: rgba(4, 18, 37, 0.96);
  border: 1px solid rgba(59, 130, 246, 0.22);
  box-shadow: 0 24px 80px rgba(59, 130, 246, 0.18);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.6rem;
}

.preview-card::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: radial-gradient(circle at top left, rgba(59, 130, 246, 0.18), transparent 28%),
    radial-gradient(circle at bottom right, rgba(59, 130, 246, 0.12), transparent 30%);
  pointer-events: none;
}

.preview-card > * {
  position: relative;
  z-index: 1;
}

.preview-badge {
  background: linear-gradient(135deg, rgba(37, 99, 235, 0.96), rgba(59, 130, 246, 0.95));
  color: #0f172a;
  padding: 0.65rem 1rem;
  border-radius: 999px;
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 0.02em;
}

.qr-preview {
  width: min(100%, 320px);
  border-radius: 2rem;
  border: 1px solid rgba(96, 165, 250, 0.22);
  padding: 1rem;
  background: #eff6ff;
}

.preview-note {
  max-width: 18rem;
  text-align: center;
  color: #bfdbfe;
  line-height: 1.75;
}

.feature-strip {
  position: relative;
  width: min(1200px, 100%);
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
}

.feature-item {
  position: relative;
  padding: 1.5rem;
  border-radius: 1.75rem;
  background: rgba(5, 18, 38, 0.86);
  border: 1px solid rgba(96, 165, 250, 0.3);
  color: #cfe8ff;
  overflow: hidden;
}

.feature-item::after {
  content: "";
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at top right, rgba(96, 165, 250, 0.2), transparent 32%),
    radial-gradient(circle at bottom left, rgba(59, 130, 246, 0.18), transparent 28%);
  pointer-events: none;
}

.feature-item strong {
  display: block;
  margin-bottom: 0.7rem;
  font-size: 1rem;
  z-index: 1;
  position: relative;
}

.feature-item span {
  color: #93c5fd;
  line-height: 1.75;
  z-index: 1;
  position: relative;
}

@media (max-width: 900px) {
  .hero-panel {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 620px) {
  .app-shell {
    padding: 2rem 1rem 1.5rem;
  }

  .hero-copy,
  .preview-card,
  .feature-item {
    border-radius: 1.5rem;
    padding: 1.5rem;
  }

  .feature-strip {
    grid-template-columns: 1fr;
  }
}
</style>
