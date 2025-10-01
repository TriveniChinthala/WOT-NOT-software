<template>
  <div class="message-generator-container">
    <div class="message-generator-card">
      <div class="header">
        <span class="icon">✨</span>
        <h1>Message Generator</h1>
      </div>
      
      <p class="description">
        Describe what kind of message you want to send, and we'll generate a template for you!
      </p>

      <!-- Prompt Input -->
      <div class="input-section">
        <label>What message do you want to create?</label>
        <textarea
          v-model="prompt"
          placeholder="e.g., I want to send Diwali wishes to my customers"
          rows="3"
        ></textarea>
      </div>

      <button
        @click="generateMessage"
        :disabled="!prompt.trim()"
        class="generate-btn"
      >
        <span>✨</span>
        Generate Message
      </button>

      <!-- Generated Message -->
      <div v-if="generatedMessage" class="output-section">
        <div class="output-header">
          <label>Generated Message (Edit as needed)</label>
          <button @click="copyToClipboard" class="copy-btn">
            {{ copied ? '✓ Copied!' : '📋 Copy' }}
          </button>
        </div>
        
        <textarea
          v-model="generatedMessage"
          rows="10"
          class="output-textarea"
        ></textarea>
        
        <div class="tip-box">
          <strong>Tip:</strong> Use placeholders like {name} and {your_name} to personalize your messages!
        </div>
      </div>

      <!-- Example Prompts -->
      <div class="examples-section">
        <h3>Try these examples:</h3>
        <div class="examples-buttons">
          <button
            v-for="example in examples"
            :key="example"
            @click="prompt = example"
            class="example-btn"
          >
            {{ example }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MessageGenerator',
  data() {
    return {
      prompt: '',
      generatedMessage: '',
      copied: false,
      examples: [
        'Diwali wishes to customers',
        'Birthday greeting',
        'Thank you message',
        'New Year wishes',
        'Event reminder'
      ]
    };
  },
  methods: {
    generateMessage() {
      const lowerPrompt = this.prompt.toLowerCase();
      let message = '';

      // Diwali wishes
      if (lowerPrompt.includes('diwali')) {
        message = 'Hello {name},\n\nWishing you a bright and prosperous Diwali! May this festival of lights bring joy, health, and success to you and your loved ones.\n\nWarm regards,\n{your_name}';
      }
      // Christmas wishes
      else if (lowerPrompt.includes('christmas') || lowerPrompt.includes('xmas')) {
        message = 'Dear {name},\n\nMerry Christmas! Wishing you peace, joy, and happiness this holiday season.\n\nBest wishes,\n{your_name}';
      }
      // New Year wishes
      else if (lowerPrompt.includes('new year')) {
        message = 'Hi {name},\n\nHappy New Year! May this year bring you new opportunities, success, and happiness.\n\nCheers to a great year ahead!\n{your_name}';
      }
      // Birthday wishes
      else if (lowerPrompt.includes('birthday')) {
        message = 'Happy Birthday {name}!\n\nWishing you a wonderful day filled with joy and celebration. May all your dreams come true!\n\nBest wishes,\n{your_name}';
      }
      // Thank you message
      else if (lowerPrompt.includes('thank')) {
        message = 'Dear {name},\n\nThank you for your continued support and trust in our services. We truly appreciate your business!\n\nBest regards,\n{your_name}';
      }
      // Announcement
      else if (lowerPrompt.includes('announcement') || lowerPrompt.includes('announce')) {
        message = 'Hello {name},\n\nWe are excited to share some important news with you! [Add your announcement here]\n\nStay tuned for more updates.\n\nBest regards,\n{your_name}';
      }
      // Reminder
      else if (lowerPrompt.includes('reminder') || lowerPrompt.includes('remind')) {
        message = 'Hi {name},\n\nThis is a friendly reminder about [event/task]. We look forward to seeing you!\n\nBest regards,\n{your_name}';
      }
      // Eid wishes
      else if (lowerPrompt.includes('eid')) {
        message = 'Eid Mubarak {name}!\n\nMay this blessed occasion bring peace, happiness, and prosperity to you and your family.\n\nWarm wishes,\n{your_name}';
      }
      // Generic greeting
      else {
        message = 'Hello {name},\n\nWe wanted to reach out and connect with you. [Add your message here]\n\nLooking forward to hearing from you!\n\nBest regards,\n{your_name}';
      }

      this.generatedMessage = message;
    },
    copyToClipboard() {
      navigator.clipboard.writeText(this.generatedMessage);
      this.copied = true;
      setTimeout(() => {
        this.copied = false;
      }, 2000);
    }
  }
};
</script>

<style scoped>
.message-generator-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #e0f2fe 0%, #ddd6fe 100%);
  padding: 2rem;
}

.message-generator-card {
  max-width: 800px;
  margin: 0 auto;
  background: white;
  border-radius: 1rem;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  padding: 2rem;
}

.header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.icon {
  font-size: 2rem;
}

.header h1 {
  font-size: 1.875rem;
  font-weight: bold;
  color: #1f2937;
  margin: 0;
}

.description {
  color: #4b5563;
  margin-bottom: 1.5rem;
}

.input-section {
  margin-bottom: 1.5rem;
}

.input-section label {
  display: block;
  font-size: 0.875rem;
  font-weight: 500;
  color: #374151;
  margin-bottom: 0.5rem;
}

.input-section textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 1px solid #d1d5db;
  border-radius: 0.5rem;
  font-size: 1rem;
  resize: vertical;
  font-family: inherit;
}

.input-section textarea:focus {
  outline: none;
  border-color: #6366f1;
  box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
}

.generate-btn {
  width: 100%;
  background: #6366f1;
  color: white;
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 0.5rem;
  font-weight: 500;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  font-size: 1rem;
  transition: background 0.2s;
}

.generate-btn:hover:not(:disabled) {
  background: #4f46e5;
}

.generate-btn:disabled {
  background: #d1d5db;
  cursor: not-allowed;
}

.output-section {
  margin-top: 2rem;
}

.output-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.75rem;
}

.output-header label {
  font-size: 0.875rem;
  font-weight: 500;
  color: #374151;
}

.copy-btn {
  background: transparent;
  border: none;
  color: #6366f1;
  font-size: 0.875rem;
  font-weight: 500;
  cursor: pointer;
  padding: 0.25rem 0.5rem;
}

.copy-btn:hover {
  color: #4f46e5;
}

.output-textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 1px solid #c7d2fe;
  border-radius: 0.5rem;
  font-size: 0.875rem;
  font-family: 'Courier New', monospace;
  background: #eef2ff;
  resize: vertical;
}

.output-textarea:focus {
  outline: none;
  border-color: #6366f1;
  box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
}

.tip-box {
  margin-top: 0.75rem;
  padding: 1rem;
  background: #dbeafe;
  border: 1px solid #bfdbfe;
  border-radius: 0.5rem;
  font-size: 0.875rem;
  color: #1e40af;
}

.examples-section {
  margin-top: 2rem;
  padding-top: 1.5rem;
  border-top: 1px solid #e5e7eb;
}

.examples-section h3 {
  font-size: 0.875rem;
  font-weight: 500;
  color: #374151;
  margin-bottom: 0.75rem;
}

.examples-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.example-btn {
  padding: 0.5rem 0.75rem;
  background: #f3f4f6;
  color: #374151;
  border: none;
  border-radius: 9999px;
  font-size: 0.875rem;
  cursor: pointer;
  transition: background 0.2s;
}

.example-btn:hover {
  background: #e5e7eb;
}
</style>