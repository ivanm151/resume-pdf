<script setup>
import { defineProps } from 'vue'
import html2canvas from 'html2canvas'
import jsPDF from 'jspdf'

const props = defineProps({
  targetId: { type: String, required: true }
})

async function exportToPDF() {
  const element = document.getElementById(props.targetId)
  if (!element) return

  const canvas = await html2canvas(element, {
    scale: 1,
    useCORS: true,
    backgroundColor: '#ffffff'
  })

  // Конвертируем в JPEG
  const imgData = canvas.toDataURL('image/jpeg', 0.8) // качество 80%

  // Создаём PDF
  const pdf = new jsPDF({
    orientation: 'portrait',
    unit: 'mm',
    format: 'a4'
  })

  const pageWidth = 210
  const pageHeight = 297
  pdf.addImage(imgData, 'JPEG', 0, 0, pageWidth, pageHeight)

  pdf.save('page.pdf')
}
</script>

<template>
  <button class="export-btn" @click="exportToPDF">
    Экспорт в PDF
  </button>
</template>

<style scoped>
.export-btn {
  position: fixed;
  bottom: 20px;
  right: 20px;
  padding: 10px 20px;
  font-size: 14px;
  cursor: pointer;
  background: white;
  border: 1px solid #000;
  border-radius: 6px;
}
</style>
