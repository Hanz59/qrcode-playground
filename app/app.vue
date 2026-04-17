<template>
  <div class="app-shell">
    <div class="hero-panel">
      <div class="hero-copy">
        <span class="eyebrow">QR Code Playground</span>
        <h1>Create stylish QR codes in seconds</h1>
        <p class="hero-text">
          Type a message or URL, choose a variant, and instantly preview an elegant QR design.
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
        <p class="preview-note">Elegant marker and dot styling for modern QR artwork.</p>
      </div>
    </div>

    <div class="feature-strip">
      <div class="feature-item">
        <strong>Instant feedback</strong>
        <span>See changes immediately as you type.</span>
      </div>
      <div class="feature-item">
        <strong>Modern shapes</strong>
        <span>Switch between default, rounded, pixelated, and dotted variants.</span>
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
  min-height: 100vh;
  padding: 3rem 1.5rem 2rem;
  color: #e2e8f0;
  background: radial-gradient(circle at top left, rgba(96, 165, 250, 0.18), transparent 25%),
    radial-gradient(circle at bottom right, rgba(236, 72, 153, 0.2), transparent 20%),
    linear-gradient(180deg, #020617 0%, #0f172a 100%);
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.hero-panel {
  width: min(1200px, 100%);
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1.2fr 0.9fr;
  gap: 2rem;
  align-items: center;
}

.hero-copy {
  padding: 2.2rem 2.4rem;
  border-radius: 2rem;
  background: rgba(15, 23, 42, 0.88);
  border: 1px solid rgba(148, 163, 184, 0.12);
  box-shadow: 0 40px 120px rgba(15, 23, 42, 0.25);
}

.eyebrow {
  display: inline-flex;
  margin-bottom: 1rem;
  padding: 0.55rem 0.95rem;
  border-radius: 999px;
  background: rgba(59, 130, 246, 0.14);
  color: #bfdbfe;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  font-size: 0.78rem;
  font-weight: 700;
}

.hero-copy h1 {
  margin: 0.75rem 0 1rem;
  font-size: clamp(2.4rem, 4vw, 3.6rem);
  line-height: 1.05;
  letter-spacing: -0.04em;
  color: #f8fafc;
}

.hero-text {
  max-width: 44rem;
  margin-bottom: 2rem;
  color: #cbd5e1;
  line-height: 1.8;
}

.controls {
  display: grid;
  gap: 1.25rem;
}

.field {
  display: grid;
  gap: 0.75rem;
  font-size: 0.95rem;
  color: #cbd5e1;
}

.field span {
  font-weight: 600;
}

.preview-card {
  position: relative;
  padding: 2rem;
  border-radius: 2rem;
  background: rgba(15, 23, 42, 0.92);
  border: 1px solid rgba(148, 163, 184, 0.14);
  box-shadow: 0 40px 100px rgba(15, 23, 42, 0.22);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.6rem;
}

.preview-badge {
  background: linear-gradient(135deg, rgba(59, 130, 246, 0.96), rgba(139, 92, 246, 0.95));
  color: #ffffff;
  padding: 0.65rem 1rem;
  border-radius: 999px;
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 0.02em;
}

.qr-preview {
  width: min(100%, 320px);
  border-radius: 1.75rem;
  border: 1px solid rgba(148, 163, 184, 0.12);
  padding: 1rem;
  background: #ffffff;
}

.preview-note {
  max-width: 18rem;
  text-align: center;
  color: #94a3b8;
  line-height: 1.7;
}

.feature-strip {
  width: min(1200px, 100%);
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
}

.feature-item {
  padding: 1.5rem;
  border-radius: 1.5rem;
  background: rgba(15, 23, 42, 0.84);
  border: 1px solid rgba(148, 163, 184, 0.1);
  color: #e2e8f0;
}

.feature-item strong {
  display: block;
  margin-bottom: 0.7rem;
  font-size: 1rem;
}

.feature-item span {
  color: #94a3b8;
  line-height: 1.75;
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
