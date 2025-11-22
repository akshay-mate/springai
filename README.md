# Spring AI Demo Application

A Spring Boot application that integrates OpenAI's GPT models to demonstrate AI-powered features like generating jokes and fetching book recommendations with intelligent summaries.

## 🎯 Project Overview

This project showcases the capabilities of **Spring AI** framework by integrating OpenAI's language models with a Spring Boot backend. It provides REST APIs that leverage AI to generate creative content and provide intelligent book recommendations.

### Key Features

- 🤖 **AI-Powered Joke Generation** - Generate jokes on any topic using OpenAI GPT
- 📚 **Book Recommendations** - Get book suggestions based on category and year
- 🔄 **Dual Response Formats** - Receive responses as plain text or structured JSON with automatic parsing
- 🔐 **Secure API Key Management** - Environment variable-based configuration for API keys
- 🚀 **RESTful API** - Easy-to-use REST endpoints for all features

## 🏗️ Project Structure

```
springai/
├── src/main/java/com/example/springaidemo/
│   ├── SpringAIDemoApplication.java          # Main Spring Boot application
│   ├── controller/
│   │   └── AIController.java                 # REST API endpoints
│   ├── service/
│   │   └── AIService.java                    # AI service logic
│   └── dto/
│       └── bookDetails.java                  # Book details DTO (Record)
├── src/main/resources/
│   └── application.properties                # Configuration file
├── pom.xml                                   # Maven dependencies
└── README.md                                 # This file
```

## 🛠️ Technologies Used

- **Java 17** - Latest LTS version
- **Spring Boot 3.2.1** - Latest stable version
- **Spring AI 0.7.1-SNAPSHOT** - AI integration framework
- **OpenAI API** - GPT language models
- **Maven** - Dependency management and build tool
- **Apache Maven 3.x** - Build automation

## 📋 Prerequisites

Before running this project, ensure you have:

- Java 17 or higher installed
- Maven 3.6 or higher
- An OpenAI API key (get one from [https://platform.openai.com/api-keys](https://platform.openai.com/api-keys))
- Git (optional, for cloning the repository)

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/akshay-mate/springai.git
cd springai
```

### 2. Set Environment Variables

Set your OpenAI API key as an environment variable:

**Windows (PowerShell):**
```powershell
$env:OPENAI_API_KEY = "your-api-key-here"
```

**Windows (Command Prompt):**
```cmd
set OPENAI_API_KEY=your-api-key-here
```

**macOS/Linux:**
```bash
export OPENAI_API_KEY="your-api-key-here"
```

### 3. Build the Project

```bash
mvn clean install
```

### 4. Run the Application

```bash
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

## 🚀 API Endpoints

### 1. Generate a Joke

**Endpoint:** `GET /api/v1/joke`

**Parameters:**
- `topic` (required) - The topic for the joke

**Example:**
```bash
curl "http://localhost:8080/api/v1/joke?topic=programming"
```

**Response:**
```
Why do programmers prefer dark mode? Because light attracts bugs!
```

---

### 2. Get Book Recommendations (Text Response)

**Endpoint:** `GET /api/v1/books`

**Parameters:**
- `category` (required) - Book category (e.g., "science fiction", "mystery", "biography")
- `year` (required) - Publication year or year range (e.g., "2023", "2020-2023")

**Example:**
```bash
curl "http://localhost:8080/api/v1/books?category=science%20fiction&year=2023"
```

**Response:**
```json
{
  "category": "Science Fiction",
  "book": "Project Hail Mary",
  "year": "2023",
  "author": "Andy Weir",
  "review": "A gripping tale of survival and ingenuity",
  "summary": "An astronaut must find a way home using science and creativity"
}
```

---

### 3. Get Book Recommendations (JSON Response with Parsing)

**Endpoint:** `GET /api/v1/booksInJSON`

**Parameters:**
- `category` (required) - Book category
- `year` (required) - Publication year

**Example:**
```bash
curl "http://localhost:8080/api/v1/booksInJSON?category=mystery&year=2023"
```

**Response:**
Returns a structured `bookDetails` object with automatic JSON parsing:
```json
{
  "category": "Mystery",
  "book": "The Thursday Murder Club",
  "year": "2023",
  "author": "Richard Osman",
  "review": "Delightfully engaging mystery",
  "summary": "A group of friends solve cold cases from their retirement home"
}
```

## 📝 Code Examples

### Using the Joke Endpoint

```java
// Simple JavaScript fetch example
fetch('http://localhost:8080/api/v1/joke?topic=space')
  .then(response => response.text())
  .then(data => console.log(data));
```

### Using the Books Endpoint

```java
// Java RestTemplate example
RestTemplate restTemplate = new RestTemplate();
String url = "http://localhost:8080/api/v1/booksInJSON?category=fantasy&year=2023";
BookDetails bookDetails = restTemplate.getForObject(url, BookDetails.class);
System.out.println("Book: " + bookDetails.book());
System.out.println("Author: " + bookDetails.author());
```

## 🔐 Security Best Practices

- **Never commit your API key** to version control
- **Use environment variables** for sensitive credentials
- The `.gitignore` file is configured to exclude:
  - `application.properties` (contains API keys)
  - `.env` files
  - Build artifacts
  - IDE-specific files

## 📦 Dependencies

Key dependencies used in this project:

```xml
<!-- Spring Boot Web Starter -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

<!-- Spring AI OpenAI Integration -->
<dependency>
    <groupId>org.springframework.experimental.ai</groupId>
    <artifactId>spring-ai-openai-spring-boot-starter</artifactId>
    <version>0.7.1-SNAPSHOT</version>
</dependency>
```

## 🧪 Testing

Run the test suite:

```bash
mvn test
```

## 📚 Learning Resources

- [Spring AI Documentation](https://docs.spring.io/spring-ai/docs/)
- [OpenAI API Documentation](https://platform.openai.com/docs/guides/gpt)
- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [PromptTemplate Guide](https://docs.spring.io/spring-ai/docs/reference/api/prompt-template.html)

## 🤝 Contributing

Contributions are welcome! Feel free to:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## ⚠️ Limitations & Notes

- This project uses the Spring AI snapshot version (0.7.1-SNAPSHOT)
- API responses depend on OpenAI's availability and rate limits
- Each API call to OpenAI incurs usage costs based on your OpenAI pricing plan
- The application requires active internet connection to reach OpenAI servers

## 📄 License

This project is open source and available under the MIT License.

## 👤 Author

**Akshay Mate**
- GitHub: [@akshay-mate](https://github.com/akshay-mate)

## 📞 Support

For issues, questions, or suggestions:

1. Open an [issue](https://github.com/akshay-mate/springai/issues) on GitHub
2. Check existing documentation and resources
3. Review OpenAI API status

---

**Happy coding! 🚀**

Last Updated: November 22, 2025

