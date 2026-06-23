<script setup>
import { ref, onMounted } from 'vue'
import { useReviewStore } from '../stores/reviewStore'
import { STORE_INFO, STORE_HIGHLIGHTS, REVIEW_EXAMPLES } from '../constants/tags'
import { Sunny, StarFilled, MagicStick, ArrowRight, InfoFilled } from '@element-plus/icons-vue'

const store = useReviewStore()

const floatingBubbles = ref([])

onMounted(() => {
  for (let i = 0; i < 8; i++) {
    floatingBubbles.value.push({
      id: i,
      left: Math.random() * 100,
      delay: Math.random() * 5,
      size: 8 + Math.random() * 16,
      duration: 8 + Math.random() * 8,
    })
  }
})

const handleStart = () => {
  store.navigateTo('select')
}
</script>

<template>
  <div class="home-page">
    <div class="bg-decoration">
      <div
        v-for="bubble in floatingBubbles"
        :key="bubble.id"
        class="bubble"
        :style="{
          left: bubble.left + '%',
          width: bubble.size + 'px',
          height: bubble.size + 'px',
          animationDelay: bubble.delay + 's',
          animationDuration: bubble.duration + 's',
        }" />
    </div>

    <div class="page-content">
      <div class="hero-section">
        <div class="badge-top">
          <el-icon class="badge-icon"><Sunny /></el-icon>
          <span>AI 智能评价助手</span>
        </div>

        <div class="cup-wrapper">
          <div class="cup-glow"></div>
          <div class="cup-container">
            <span class="cup-emoji">☕</span>
          </div>
          <div class="rating-pill">
            <el-icon class="star-icon"><StarFilled /></el-icon>
            <span>{{ STORE_INFO.rating }}</span>
          </div>
          <div class="cup-shadow"></div>
        </div>

        <h1 class="hero-title">{{ STORE_INFO.name }}</h1>
        <p class="hero-subtitle">{{ STORE_INFO.location }} · 一杯好茶，值得被看见</p>

        <div class="tags-row">
          <span class="tag-chip">🍃 鲜奶现煮</span>
          <span class="tag-chip">✨ 高颜值</span>
          <span class="tag-chip">🌿 天然原料</span>
        </div>
      </div>

      <div class="stats-card">
        <p class="stats-intro">店铺信息</p>
        <div class="stats-grid">
          <div
            v-for="item in STORE_HIGHLIGHTS"
            :key="item.label"
            class="stat-item">
            <div class="stat-icon">{{ item.icon }}</div>
            <div class="stat-value">{{ item.value }}</div>
            <div class="stat-label">{{ item.label }}</div>
          </div>
        </div>
      </div>

      <div class="hot-reviews">
        <div class="section-header">
          <div>
            <h3 class="section-title">评价灵感示例</h3>
            <p class="section-note">风格参考，非真实用户评价</p>
          </div>
          <span class="section-badge">示例</span>
        </div>

        <div class="review-list">
          <div
            v-for="(review, idx) in REVIEW_EXAMPLES"
            :key="idx"
            class="review-item">
            <div class="review-avatar">{{ review.avatar }}</div>
            <div class="review-content">
              <div class="review-header">
                <span class="review-user">{{ review.user }}</span>
                <div class="review-stars">
                  <el-icon
                    v-for="i in review.stars"
                    :key="i"
                    class="star-icon"><StarFilled /></el-icon>
                </div>
              </div>
              <p class="review-text">{{ review.text }}</p>
            </div>
          </div>
        </div>
      </div>

      <div class="ai-section">
        <div class="ai-header">
          <div class="ai-icon-wrapper">
            <el-icon class="ai-icon"><MagicStick /></el-icon>
          </div>
          <span class="ai-title">AI 一键生成专属评价</span>
        </div>

        <div class="steps-row">
          <div class="step-item">
            <div class="step-number">1</div>
            <div class="step-text">选择感受</div>
          </div>
          <div class="step-arrow">→</div>
          <div class="step-item">
            <div class="step-number">2</div>
            <div class="step-text">选择平台</div>
          </div>
          <div class="step-arrow">→</div>
          <div class="step-item">
            <div class="step-number">3</div>
            <div class="step-text">一键生成</div>
          </div>
        </div>
      </div>

      <button class="start-button" @click="handleStart">
        <span class="btn-text">立即生成我的评价</span>
        <span class="btn-icon-wrapper">
          <el-icon class="btn-icon"><ArrowRight /></el-icon>
        </span>
      </button>

      <div class="footer-tips">
        <el-icon class="tip-icon"><InfoFilled /></el-icon>
        <span>由阿里云百炼 qwen-plus 提供 AI 能力</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home-page {
  min-height: 100vh;
  max-width: 480px;
  margin: 0 auto;
  position: relative;
  overflow: hidden;
  background: linear-gradient(180deg, #fdfbf7 0%, #f9f2e6 50%, #fef3c7 100%);
}

.bg-decoration {
  position: absolute;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
}

.bubble {
  position: absolute;
  bottom: -50px;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.8) 0%, rgba(255, 255, 255, 0.2) 100%);
  border-radius: 50%;
  animation: float-up linear infinite;
  opacity: 0.6;
}

@keyframes float-up {
  0% { transform: translateY(0) rotate(0deg); opacity: 0; }
  10% { opacity: 0.6; }
  90% { opacity: 0.6; }
  100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
}

.page-content {
  position: relative;
  z-index: 1;
  padding: 24px 20px 32px;
}

.hero-section {
  text-align: center;
  margin-bottom: 24px;
}

.badge-top {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 6px 14px;
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(201, 153, 75, 0.2);
  border-radius: 20px;
  font-size: 12px;
  color: #93632c;
  font-weight: 500;
  margin-bottom: 20px;
  box-shadow: 0 2px 8px rgba(201, 153, 75, 0.1);
}

.badge-icon {
  color: #f59e0b;
  font-size: 14px;
}

.cup-wrapper {
  position: relative;
  display: inline-block;
  margin-bottom: 20px;
}

.cup-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 180px;
  height: 180px;
  background: radial-gradient(circle, rgba(251, 191, 36, 0.4) 0%, transparent 70%);
  border-radius: 50%;
  animation: pulse-glow 2s ease-in-out infinite;
}

@keyframes pulse-glow {
  0%, 100% { transform: translate(-50%, -50%) scale(1); opacity: 0.6; }
  50% { transform: translate(-50%, -50%) scale(1.1); opacity: 0.8; }
}

.cup-container {
  position: relative;
  width: 120px;
  height: 120px;
  background: linear-gradient(135deg, #fcd34d 0%, #f59e0b 50%, #d97706 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow:
    0 10px 30px rgba(245, 158, 11, 0.4),
    inset 0 -4px 8px rgba(217, 119, 6, 0.3),
    inset 0 4px 8px rgba(252, 211, 77, 0.5);
  animation: float 3s ease-in-out infinite;
}

.cup-emoji {
  font-size: 60px;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.1));
}

.rating-pill {
  position: absolute;
  top: 5px;
  right: -5px;
  background: linear-gradient(135deg, #10b981, #059669);
  color: white;
  padding: 4px 10px;
  border-radius: 12px;
  font-size: 12px;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 2px;
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);
  z-index: 2;
}

.star-icon {
  color: #fbbf24;
  font-size: 12px;
}

.cup-shadow {
  position: absolute;
  bottom: -15px;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 12px;
  background: radial-gradient(ellipse, rgba(217, 119, 6, 0.2) 0%, transparent 70%);
  border-radius: 50%;
  filter: blur(4px);
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}

.hero-title {
  font-size: 32px;
  font-weight: 800;
  margin: 0 0 8px;
  background: linear-gradient(135deg, #c9994b 0%, #f59e0b 50%, #d97706 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  letter-spacing: -0.5px;
}

.hero-subtitle {
  color: #93632c;
  font-size: 14px;
  margin: 0 0 16px;
  font-weight: 500;
}

.tags-row {
  display: flex;
  justify-content: center;
  gap: 8px;
  flex-wrap: wrap;
}

.tag-chip {
  padding: 4px 12px;
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(201, 153, 75, 0.2);
  border-radius: 16px;
  font-size: 11px;
  color: #775029;
  font-weight: 500;
}

.stats-card {
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 8px 32px rgba(201, 153, 75, 0.12);
  border: 1px solid rgba(255, 255, 255, 0.5);
}

.stats-intro {
  font-size: 14px;
  font-weight: 600;
  color: #775029;
  margin: 0 0 16px;
  text-align: center;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
}

.stat-item {
  text-align: center;
  padding: 12px 8px;
  background: rgba(252, 211, 77, 0.08);
  border-radius: 12px;
  border: 1px solid rgba(201, 153, 75, 0.12);
}

.stat-icon {
  font-size: 20px;
  margin-bottom: 6px;
}

.stat-value {
  font-size: 15px;
  font-weight: 700;
  color: #c9994b;
  margin-bottom: 4px;
}

.stat-label {
  font-size: 11px;
  color: #93632c;
  font-weight: 500;
}

.hot-reviews {
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 8px 32px rgba(201, 153, 75, 0.12);
  border: 1px solid rgba(255, 255, 255, 0.5);
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 16px;
}

.section-title {
  font-size: 16px;
  font-weight: 700;
  color: #775029;
  margin: 0 0 4px;
}

.section-note {
  font-size: 11px;
  color: #93632c;
  margin: 0;
  opacity: 0.8;
}

.section-badge {
  padding: 2px 8px;
  background: rgba(201, 153, 75, 0.15);
  color: #93632c;
  font-size: 10px;
  font-weight: 600;
  border-radius: 8px;
  flex-shrink: 0;
}

.review-list {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.review-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px;
  background: rgba(252, 211, 77, 0.1);
  border-radius: 12px;
  border: 1px solid rgba(252, 211, 77, 0.2);
}

.review-avatar {
  font-size: 24px;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: white;
  border-radius: 50%;
  flex-shrink: 0;
}

.review-content {
  flex: 1;
  min-width: 0;
}

.review-header {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 4px;
}

.review-user {
  font-size: 13px;
  font-weight: 600;
  color: #775029;
}

.review-stars {
  display: flex;
  gap: 1px;
}

.review-text {
  font-size: 12px;
  color: #93632c;
  margin: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.ai-section {
  background: linear-gradient(135deg, rgba(252, 211, 77, 0.15) 0%, rgba(245, 158, 11, 0.1) 100%);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  padding: 20px;
  margin-bottom: 24px;
  border: 1px solid rgba(245, 158, 11, 0.2);
  box-shadow: 0 8px 32px rgba(245, 158, 11, 0.1);
}

.ai-header {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 16px;
}

.ai-icon-wrapper {
  width: 32px;
  height: 32px;
  background: linear-gradient(135deg, #f59e0b, #d97706);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(245, 158, 11, 0.3);
}

.ai-icon {
  color: white;
  font-size: 16px;
}

.ai-title {
  font-size: 15px;
  font-weight: 700;
  color: #775029;
}

.steps-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.step-item {
  flex: 1;
  text-align: center;
}

.step-number {
  width: 36px;
  height: 36px;
  background: linear-gradient(135deg, #c9994b, #d97706);
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 16px;
  margin: 0 auto 8px;
  box-shadow: 0 4px 12px rgba(201, 153, 75, 0.3);
}

.step-text {
  font-size: 12px;
  color: #775029;
  font-weight: 600;
}

.step-arrow {
  color: #c9994b;
  font-size: 20px;
  font-weight: 700;
  margin: 0 8px 20px;
}

.start-button {
  width: 100%;
  height: 56px;
  background: linear-gradient(135deg, #f59e0b 0%, #d97706 50%, #b45309 100%);
  color: white;
  border: none;
  border-radius: 16px;
  font-size: 17px;
  font-weight: 700;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  box-shadow: 0 8px 24px rgba(245, 158, 11, 0.4);
  transition: all 0.3s ease;
}

.start-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 32px rgba(245, 158, 11, 0.5);
}

.start-button:active {
  transform: translateY(0);
}

.btn-text,
.btn-icon-wrapper {
  position: relative;
  z-index: 1;
}

.btn-icon-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 24px;
  height: 24px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
}

.btn-icon {
  font-size: 14px;
  color: white;
}

.footer-tips {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4px;
  margin-top: 20px;
  font-size: 11px;
  color: #93632c;
  opacity: 0.7;
}

.tip-icon {
  font-size: 12px;
}
</style>
