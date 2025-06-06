<script lang="ts">
  let messages = [
    {
      role: 'assistant',
      content: 'Hello! I\'m GC Assistant, your virtual guide to Gordon College, Zambales. How can I help you today? You can ask me about:\n\n• Admission Requirements\n• Course Programs\n• School Facilities\n• Academic Calendar\n• Student Services'
    }
  ];
  
  let userInput = '';
  let isTyping = false;

  const quickQuestions = [
    {
      icon: '🎓',
      question: 'How do I apply for admission?',
      category: 'Admissions'
    },
    {
      icon: '📚',
      question: 'What courses are available?',
      category: 'Academics'
    },
    {
      icon: '📍',
      question: 'Where is the campus located?',
      category: 'Location'
    },
    {
      icon: '💰',
      question: 'What are the tuition fees?',
      category: 'Finance'
    }
  ];

  function handleSubmit() {
    if (!userInput.trim()) return;
    
    // Add user message
    messages = [...messages, {
      role: 'user',
      content: userInput
    }];
    
    // Clear input and show typing indicator
    const question = userInput;
    userInput = '';
    isTyping = true;
    
    // Simulate response (TODO: Replace with actual API call)
    setTimeout(() => {
      isTyping = false;
      messages = [...messages, {
        role: 'assistant',
        content: getPlaceholderResponse(question)
      }];
    }, 1500);
  }

  function handleQuickQuestion(question: string) {
    userInput = question;
    handleSubmit();
  }

  function getPlaceholderResponse(question: string) {
    // Temporary responses based on keywords
    if (question.toLowerCase().includes('admission')) {
      return 'To apply for admission at Gordon College:\n\n1. Complete the online application form\n2. Submit required documents:\n   • Form 138 (Report Card)\n   • Certificate of Good Moral Character\n   • 2x2 ID Pictures\n   • Birth Certificate\n3. Pay the application fee\n4. Take the entrance exam\n\nFor more details, visit our Admissions Office or call (047) 222-XXXX.';
    }
    if (question.toLowerCase().includes('courses')) {
      return 'Gordon College offers various undergraduate programs including:\n\n• Bachelor of Science in Information Technology\n• Bachelor of Science in Business Administration\n• Bachelor of Elementary Education\n• Bachelor of Secondary Education\n• Bachelor of Science in Criminology\n\nWould you like specific information about any of these programs?';
    }
    if (question.toLowerCase().includes('location')) {
      return 'Gordon College is located at Rizal St., East Tapinac, Olongapo City, Zambales. We are accessible via public transportation and just a few minutes away from SM City Olongapo.';
    }
    return 'I understand you\'re asking about ' + question + '. Let me connect you with the right department for more detailed information. You can also visit our admin office or call (047) 222-XXXX.';
  }
</script>

<div class="chat-container">
  <div class="welcome-banner">
    <img src="/gordon-seal.png" alt="Gordon College Seal" class="school-seal" />
    <h2>Welcome to Gordon College Virtual Assistant</h2>
    <p>Ask me anything about our institution</p>
  </div>

  <div class="ask-gc">
    <p class="section-label">Ask GC:</p>
    <div class="questions-grid">
      {#each quickQuestions as { icon, question, category }}
        <button 
          class="ask-gc-btn"
          on:click={() => handleQuickQuestion(question)}
        >
          <span class="ask-gc-icon">{icon}</span>
          <div class="ask-gc-content">
            <span class="ask-gc-category">{category}</span>
            <span class="ask-gc-question">{question}</span>
          </div>
        </button>
      {/each}
    </div>
  </div>

  <div class="chat-messages" id="chat-messages">
    {#each messages as message}
      <div class="message {message.role}">
        {#if message.role === 'assistant'}
          <div class="avatar">
            <img src="/gc-avatar.png" alt="GC Assistant" />
          </div>
        {/if}
        <div class="message-content">
          {#if message.role === 'assistant'}
            <span class="badge">GC Assistant</span>
          {/if}
          <p>{message.content}</p>
        </div>
      </div>
    {/each}
    {#if isTyping}
      <div class="message assistant">
        <div class="avatar">
          <img src="/gc-avatar.png" alt="GC Assistant" />
        </div>
        <div class="typing-indicator">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    {/if}
  </div>

  <form class="chat-input" on:submit|preventDefault={handleSubmit}>
    <input
      type="text"
      bind:value={userInput}
      placeholder="Type your question about Gordon College..."
      aria-label="Chat input"
    />
    <button type="submit" class="send-button" aria-label="Send message">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="send-icon">
        <path d="M3.478 2.405a.75.75 0 00-.926.94l2.432 7.905H13.5a.75.75 0 010 1.5H4.984l-2.432 7.905a.75.75 0 00.926.94 60.519 60.519 0 0018.445-8.986.75.75 0 000-1.218A60.517 60.517 0 003.478 2.405z" />
      </svg>
    </button>
  </form>
</div>

<style>
  .chat-container {
    display: flex;
    flex-direction: column;
    height: calc(100vh - 130px);
    background: var(--surface);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-md);
    overflow: hidden;
  }

  .welcome-banner {
    background: var(--primary);
    color: white;
    padding: var(--spacing-xl);
    text-align: center;
  }

  .school-seal {
    width: 80px;
    height: 80px;
    margin-bottom: var(--spacing-md);
  }

  .welcome-banner h2 {
    font-size: 1.5rem;
    margin-bottom: var(--spacing-xs);
  }

  .welcome-banner p {
    color: var(--secondary);
  }

  .ask-gc {
    padding: var(--spacing-lg);
    background: white;
    border-bottom: 1px solid var(--border);
  }

  .section-label {
    font-size: 1rem;
    color: var(--primary);
    font-weight: 600;
    margin-bottom: var(--spacing-md);
  }

  .questions-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: var(--spacing-md);
  }

  .ask-gc-btn {
    display: flex;
    align-items: center;
    gap: var(--spacing-md);
    background: var(--surface);
    border: 1px solid var(--border);
    padding: var(--spacing-md);
    border-radius: var(--radius-md);
    text-align: left;
    transition: all 0.2s;
    width: 100%;
  }

  .ask-gc-btn:hover {
    background: var(--primary);
    color: white;
    border-color: var(--primary);
    transform: translateY(-2px);
  }

  .ask-gc-icon {
    font-size: 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    background: white;
    border-radius: var(--radius-md);
    flex-shrink: 0;
  }

  .ask-gc-btn:hover .ask-gc-icon {
    background: rgba(255, 255, 255, 0.1);
  }

  .ask-gc-content {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  .ask-gc-category {
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    opacity: 0.7;
  }

  .ask-gc-question {
    font-size: 0.875rem;
    font-weight: 500;
  }

  .chat-messages {
    flex: 1;
    overflow-y: auto;
    padding: var(--spacing-lg);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
  }

  .message {
    display: flex;
    gap: var(--spacing-md);
    max-width: 80%;
  }

  .message.user {
    margin-left: auto;
    flex-direction: row-reverse;
  }

  .avatar {
    width: 40px;
    height: 40px;
    border-radius: var(--radius-full);
    overflow: hidden;
    flex-shrink: 0;
  }

  .avatar img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .message-content {
    padding: var(--spacing-md);
    border-radius: var(--radius-md);
    box-shadow: var(--shadow-sm);
    white-space: pre-line;
  }

  .message-content .badge {
    display: inline-block;
    margin-bottom: var(--spacing-xs);
  }

  .user .message-content {
    background: var(--primary);
    color: white;
  }

  .assistant .message-content {
    background: white;
    border: 1px solid var(--border);
  }

  .typing-indicator {
    background: white;
    padding: var(--spacing-md);
    border-radius: var(--radius-md);
    border: 1px solid var(--border);
    display: flex;
    gap: 4px;
  }

  .typing-indicator span {
    width: 8px;
    height: 8px;
    background: var(--text-light);
    border-radius: var(--radius-full);
    animation: typing 1.4s infinite;
    opacity: 0.4;
  }

  .typing-indicator span:nth-child(2) { animation-delay: 0.2s; }
  .typing-indicator span:nth-child(3) { animation-delay: 0.4s; }

  @keyframes typing {
    0%, 100% { opacity: 0.4; }
    50% { opacity: 1; }
  }

  .chat-input {
    display: flex;
    gap: var(--spacing-sm);
    padding: var(--spacing-md);
    background: white;
    border-top: 1px solid var(--border);
  }

  input {
    flex: 1;
    padding: var(--spacing-md);
    border: 1px solid var(--border);
    border-radius: var(--radius-full);
    font-size: 1rem;
    transition: all 0.2s;
  }

  input:focus {
    outline: none;
    border-color: var(--primary);
    box-shadow: 0 0 0 2px rgba(0, 51, 102, 0.1);
  }

  .send-button {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 2.5rem;
    height: 2.5rem;
    border-radius: var(--radius-full);
    background: var(--primary);
    color: white;
    transition: all 0.2s;
  }

  .send-button:hover {
    background: var(--primary-light);
  }

  .send-icon {
    width: 1.25rem;
    height: 1.25rem;
  }
</style> 