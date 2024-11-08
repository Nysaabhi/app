<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Deep Chatbot</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #FFD700;
            --secondary-color: #FDB931;
            --background-dark: #1a1a1f;
            --text-light: #ffffff;
            --text-dark: #000000;
            --accent-gradient: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: var(--background-dark);
            color: var(--text-light);
            line-height: 1.6;
            min-height: 100vh;
            overflow-x: hidden;
        }
        
        .header {
            padding: 8px 16px;
            background: rgba(26, 26, 31, 0.95);
            position: fixed;
            width: 100%;
            top: 0;
            left: 0;
            z-index: 30;
            border-bottom: 2px solid var(--primary-color);
            backdrop-filter: blur(10px);
            height: 60px;
        }
        
        .header-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 100%;
        }
        
        .logo {
            font-size: 1.8em;
            font-weight: 900;
            background: var(--accent-gradient);
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: 1.2px;
        }
        
        .wallet {
            padding: 10px 20px;
            background: var(--accent-gradient);
            border: none;
            border-radius: 50px;
            color: var(--text-dark);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.95em;
        }
        
        .chatbot-container {
            position: fixed;
            top: 60px;
            left: 0;
            right: 0;
            bottom: 60px;
            background: rgba(26, 26, 31, 0.95);
            display: flex;
            flex-direction: column;
        }
        
        .chat-header {
            padding: 15px;
            background: linear-gradient(135deg, rgba(255, 215, 0, 0.1), rgba(253, 185, 49, 0.1));
            border-bottom: 1px solid rgba(255, 215, 0, 0.2);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .chat-status {
            display: flex;
            align-items: center;
            color: var(--primary-color);
            font-weight: 600;
        }
        
        .status-dot {
            width: 8px;
            height: 8px;
            background: var(--primary-color);
            border-radius: 50%;
            margin-right: 8px;
            animation: pulse 2s infinite;
        }
        
        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
        }
        
        .message {
            display: flex;
            gap: 12px;
            max-width: 85%;
            margin-bottom: 16px;
            animation: messageSlide 0.3s ease-out;
        }
        
        .bot-message {
            align-self: flex-start;
        }
        
        .user-message {
            align-self: flex-end;
            flex-direction: row-reverse;
        }
        
        .message-avatar {
            width: 36px;
            height: 36px;
            background: rgba(255, 215, 0, 0.1);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--primary-color);
        }
        
        .message-content {
            background: rgba(255, 255, 255, 0.05);
            padding: 12px 16px;
            border-radius: 16px;
            color: var(--text-light);
        }
        
        .user-message .message-content {
            background: rgba(255, 215, 0, 0.1);
        }

        .service-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            padding: 15px;
            margin-top: 10px;
            border: 1px solid rgba(255, 215, 0, 0.2);
        }

        .service-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .service-rating {
            display: flex;
            align-items: center;
            color: var(--primary-color);
        }

        .service-details {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-top: 10px;
        }

        .service-detail-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .service-actions {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }

        .service-button {
            padding: 8px 15px;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s ease;
        }

        .book-button {
            background: var(--accent-gradient);
            color: var(--text-dark);
        }

        .contact-button {
            background: rgba(255, 215, 0, 0.1);
            color: var(--primary-color);
            border: 1px solid var(--primary-color);
        }
        
        .chat-input-container {
            padding: 16px;
            background: rgba(26, 26, 31, 0.98);
            border-top: 1px solid rgba(255, 215, 0, 0.1);
            display: flex;
            gap: 12px;
            align-items: center;
        }
        
        #chatInput {
            flex: 1;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 215, 0, 0.2);
            border-radius: 12px;
            padding: 12px 16px;
            color: var(--text-light);
            font-size: 0.95em;
        }
        
        .input-actions {
            display: flex;
            gap: 8px;
        }
        
        .input-actions button {
            background: none;
            border: none;
            color: rgba(255, 215, 0, 0.7);
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: all 0.3s ease;
        }
        
        .category-popup {
            position: absolute;
            bottom: 80px;
            left: 16px;
            right: 16px;
            background: rgba(26, 26, 31, 0.98);
            border: 1px solid rgba(255, 215, 0, 0.2);
            border-radius: 12px;
            padding: 16px;
            display: none;
        }

        .category-popup.active {
            display: block;
            animation: slideUp 0.3s ease-out;
        }

        .category-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin-top: 12px;
        }

        .category-item {
            background: rgba(255, 215, 0, 0.1);
            border: 1px solid rgba(255, 215, 0, 0.2);
            border-radius: 8px;
            padding: 12px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .category-item:hover {
            background: rgba(255, 215, 0, 0.2);
        }
        
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            height: 60px;
            background: rgba(26, 26, 31, 0.98);
            padding: 8px 0;
            border-top: 1px solid rgba(255, 215, 0, 0.2);
        }
        
        .nav-container {
            display: flex;
            justify-content: space-around;
            align-items: center;
            height: 100%;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: #fff;
            transition: all 0.3s ease;
            padding: 5px;
            cursor: pointer;
        }
        
        .nav-item i {
            font-size: 20px;
            margin-bottom: 4px;
        }
        
        .nav-item span {
            font-size: 12px;
        }
        
        .nav-item.active i {
            color: var(--primary-color);
        }
        
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }
        
        @keyframes messageSlide {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        @media (max-width: 768px) {
            .header {
                padding: 8px 12px;
            }
            
            .logo {
                font-size: 1.5em;
            }
            
            .chat-messages {
                padding: 15px;
            }
            
            .message {
                max-width: 90%;
            }
            
            .nav-item i {
                font-size: 18px;
            }
            
            .nav-item span {
                font-size: 11px;
            }
        }

                body > h1:first-of-type:not(.heading) {
          display: none !important;
        }
        
        /* Alternative method if the above doesn't work */
        .markdown-body h1:first-child {
          display: none !important;
        }
        
        /* If the number appears in a different container */
        .position-relative h1:first-child {
          display: none !important;
        }

    </style>
</head>
<body>
    <header class="header">
        <div class="header-content">
            <div class="logo">Deep</div>
            <button class="wallet">
                <i class="fas fa-wallet"></i>
              Wallet
            </button>
        </div>
    </header>

    <div class="chatbot-container">
        <div class="chat-header">
            <div class="chat-status">
                <span class="status-dot"></span>
                Deep AI Assistant
            </div>
        </div>
        
        <div class="chat-messages" id="chatMessages">
            <div class="message bot-message">
                <div class="message-avatar">
                    <i class="fas fa-robot"></i>
                </div>
                <div class="message-content">
                    <p>Hello! I'm your On-Demand services assistant. How can I help you today? You can search for services or select from our categories.</p>
                </div>
            </div>
        </div>

        <div class="category-popup" id="categoryPopup">
            <h3>Select Service Category</h3>
            <div class="category-grid">
                <div class="category-item" data-category="plumber">
                    <i class="fas fa-wrench"></i>
                    <p>Plumber</p>
                </div>
                <div class="category-item" data-category="electrician">
                    <i class="fas fa-bolt"></i>
                    <p>Electrician</p>
                </div>
                <div class="category-item" data-category="carpenter">
                    <i class="fas fa-hammer"></i>
                    <p>Carpenter</p>
                </div>
                <div class="category-item" data-category="painter">
                    <i class="fas fa-paint-roller"></i>
                    <p>Painter</p>
                </div>
                <div class="category-item" data-category="cleaner">
                    <i class="fas fa-broom"></i>
                    <p>Cleaner</p>
                </div>
                <div class="category-item" data-category="designer">
                    <i class="fas fa-pencil-ruler"></i>
                    <p>Designer</p>
                </div>
            </div>
        </div>
        
        <div class="chat-input-container">
            <input type="text" id="chatInput" placeholder="Search for services or ask a question..." />
            <div class="input-actions">
                <button class="select-input" id="categoryButton">
                    <i class="fas fa-th-large"></i>
                </button>
                <button class="send-message" id="sendButton">
                    <i class="fas fa-paper-plane"></i>
                </button>
            </div>
        </div>
    </div>

    <nav class="bottom-nav">
        <div class="nav-container">
            <div class="nav-item active" data-page="maintenance">
                <i class="fas fa-tools"></i>
                <span>Maintenance</span>
            </div>
            <div class="nav-item" data-page="deals">
                <i class="fas fa-ticket"></i>
                <span>Deals</span>
            </div>
            <div class="nav-item" data-page="filter">
                <i class="fas fa-filter"></i>
                <span>Filter & Sort</span>
            </div>
            <div class="nav-item" data-page="bookings">
                <i class="fas fa-calendar-alt"></i>
                <span>Bookings</span>
            </div>
            <div class="nav-item" data-page="city">
                <i class="fas fa-location"></i>
                <span>City</span>
            </div>
        </div>
    </nav>
    
                <script>
                    const chatMessages = document.getElementById('chatMessages');
                    const chatInput = document.getElementById('chatInput');
                    const categoryPopup = document.getElementById('categoryPopup');
                    const categoryButton = document.getElementById('categoryButton');
                    const sendButton = document.getElementById('sendButton');
                    
                    // Sample service providers data
                    const serviceProvidersData = [
                      {
                        id: 1,
                        name: "Rajesh Kumar",
                        category: "plumber",
                        city: "Delhi",
                        pincode: "110001",
                        rating: 4.8,
                        experience: "8 years",
                        price: "₹500/hour",
                        phone: "+91-9876543210",
                        email: "rajesh@example.com",
                        availability: "Mon-Sat",
                        reviews: 156,
                        skills: ["Pipe Fitting", "Leak Repair", "Bathroom Installation"]
                      },
                      // Add more service providers here
                    ];
                    
                    let currentCategory = null;
                    
                    // Function to display service provider cards
                    function displayServiceProviders(category) {
                      chatMessages.innerHTML = '';
                      const filteredProviders = serviceProvidersData.filter(provider => provider.category === category);
                    
                      filteredProviders.forEach(provider => {
                        const serviceCard = document.createElement('div');
                        serviceCard.classList.add('service-card');
                    
                        serviceCard.innerHTML = `
                          <div class="service-header">
                            <h3>${provider.name}</h3>
                            <div class="service-rating">
                              <i class="fas fa-star"></i>
                              <span>${provider.rating}</span>
                            </div>
                          </div>
                          <div class="service-details">
                            <div class="service-detail-item">
                              <i class="fas fa-map-marker-alt"></i>
                              <span>${provider.city}, ${provider.pincode}</span>
                            </div>
                            <div class="service-detail-item">
                              <i class="fas fa-clock"></i>
                              <span>${provider.availability}</span>
                            </div>
                            <div class="service-detail-item">
                              <i class="fas fa-money-bill-alt"></i>
                              <span>${provider.price}</span>
                            </div>
                            <div class="service-detail-item">
                              <i class="fas fa-briefcase"></i>
                              <span>${provider.experience}</span>
                            </div>
                          </div>
                          <div class="service-actions">
                            <button class="service-button book-button">Book Now</button>
                            <button class="service-button contact-button">
                              <i class="fas fa-phone"></i>
                              Contact
                            </button>
                          </div>
                        `;
                    
                        chatMessages.appendChild(serviceCard);
                      });
                    
                      if (filteredProviders.length === 0) {
                        const noResultsAlert = document.createElement('div');
                        noResultsAlert.classList.add('service-card');
                        noResultsAlert.innerHTML = `
                          <div class="service-header">
                            <h3>No results found</h3>
                            <div class="service-rating">
                              <i class="fas fa-exclamation-circle"></i>
                            </div>
                          </div>
                          <div class="service-details">
                            <div class="service-detail-item">
                              <span>Sorry, we couldn't find any service providers for the selected category.</span>
                            </div>
                          </div>
                        `;
                        chatMessages.appendChild(noResultsAlert);
                      }
                    }
                    
                    // Function to handle category selection
                    function handleCategorySelection(category) {
                      currentCategory = category;
                      displayServiceProviders(category);
                      categoryPopup.classList.remove('active');
                    }
                    
                    // Event listeners
                    categoryButton.addEventListener('click', () => {
                      categoryPopup.classList.add('active');
                    });
                    
                    categoryPopup.addEventListener('click', (event) => {
                      if (event.target.classList.contains('category-item')) {
                        const selectedCategory = event.target.dataset.category;
                        handleCategorySelection(selectedCategory);
                      }
                    });
                    
                    sendButton.addEventListener('click', () => {
                      const userInput = chatInput.value.trim();
                      if (userInput) {
                        const userMessage = document.createElement('div');
                        userMessage.classList.add('message', 'user-message');
                        userMessage.innerHTML = `
                          <div class="message-avatar">
                            <i class="fas fa-user"></i>
                          </div>
                          <div class="message-content">
                            <p>${userInput}</p>
                          </div>
                        `;
                        chatMessages.appendChild(userMessage);
                    
                        // Process user input and generate a response
                        const botResponse = processUserInput(userInput);
                        const botMessage = document.createElement('div');
                        botMessage.classList.add('message', 'bot-message');
                        botMessage.innerHTML = `
                          <div class="message-avatar">
                            <i class="fas fa-robot"></i>
                          </div>
                          <div class="message-content">
                            <p>${botResponse}</p>
                          </div>
                        `;
                        chatMessages.appendChild(botMessage);
                    
                        chatInput.value = '';
                        chatMessages.scrollTop = chatMessages.scrollHeight;
                      }
                    });
                    
                    function processUserInput(input) {
                      // Implement your logic to process the user's input and generate a response
                      if (input.toLowerCase().includes('hello')) {
                        return "Hello! How can I assist you today?";
                      } else if (input.toLowerCase().includes('category')) {
                        categoryPopup.classList.add('active');
                        return "Please select a service category from the list.";
                      } else {
                        // Search for matching service providers based on the user's input
                        const keywords = input.toLowerCase().split(' ');
                        const matchingProviders = serviceProvidersData.filter(provider => {
                          return keywords.some(keyword => (
                            provider.name.toLowerCase().includes(keyword) ||
                            provider.category.toLowerCase().includes(keyword) ||
                            provider.city.toLowerCase().includes(keyword) ||
                            provider.skills.some(skill => skill.toLowerCase().includes(keyword))
                          ));
                        });
                    
                        if (matchingProviders.length > 0) {
                          currentCategory = null;
                          displayServiceProviders(matchingProviders);
                          return "Here are the service providers that match your search:";
                        } else {
                          return "Sorry, I couldn't find any service providers that match your search. Please try again with a different query.";
                        }
                      }
                    }
                    </script>
                </body>
