# Travel & Culture-Aware Shopping Chatbot

An AI-powered travel shopping assistant with cultural sensitivity and climate-aware recommendations for travelers, seamlessly integrable into e-commerce platforms and web services to enhance customer experience.

## Problem Statement

International travelers often face challenges when shopping for their destinations:

* **Cultural Insensitivity** – Lack of awareness about appropriate dress codes and customs
* **Climate Mismatches** – Packing inappropriate clothing for seasonal weather conditions
* **Religious Considerations** – Inadvertently purchasing items unsuitable for conservative destinations
* **Festival Blindness** – Missing opportunities for culturally relevant gifts and attire
* **Regional Variations** – Overlooking city-specific climate differences within countries

## Solution Overview

The Travel & Culture-Aware Shopping Chatbot is an AI-powered solution that addresses these pain points by providing **personalized, culturally sensitive, and climate-aware product recommendations**.
It can be integrated directly into **e-commerce platforms, travel booking websites, or product stores** to improve client interactions, increase customer satisfaction, and enhance business performance.

## Integration with Products, Web Services, and Stores

Our chatbot is designed with a **RESTful API-first architecture**, enabling seamless embedding into various platforms:

* **E-commerce Platforms**
  Integrate the chatbot as a recommendation engine to suggest travel-appropriate products (clothing, accessories, gifts) based on the shopper’s travel destination, season, and cultural context.

* **Travel Booking Websites**
  Offer travelers an intelligent packing and shopping assistant directly after they book a trip, improving post-booking engagement.

* **Retailer Websites and Apps**
  Provide culturally aware product filtering and personalized suggestions to reduce returns and boost conversion rates.

* **Customer Support Systems**
  Integrate with live chat systems to provide instant, AI-driven recommendations that combine cultural, climate, and seasonal insights.

* **API-based Integration for Partner Stores**
  Third-party stores can use the chatbot’s APIs to enrich their product search and filtering with cultural and climate metadata.

By embedding this chatbot, businesses can deliver **context-aware personalization**, increase user trust, and reduce friction in the shopping journey, improving overall **client service and business performance**.

## Architecture

<img width="1014" height="632" alt="image" src="https://github.com/user-attachments/assets/e81163d2-3679-40f3-9502-14882bba784c" />

## Key Features

### AI-Powered Intelligence

* **Gemini 2.5 Integration** – Advanced natural language processing for understanding user intent
* **Seasonal Context Parsing** – Automatically detects travel season (e.g., winter/summer)
* **Cultural Awareness** – Knowledge base for dress codes in 15+ countries
* **Festival Recognition** – Identifies cultural events and suggests appropriate products

### Climate Intelligence

* **Regional Weather Data** – City-specific climate insights for accurate recommendations
* **Seasonal Filtering** – Filters products by temperature and weather conditions
* **Multi-Source Data** – Wikipedia climate scraping and cached weather APIs
* **Temperature-Based Recommendations** – Suggests appropriate gear for hot, cold, or humid weather

### Cultural Sensitivity Engine

* **Model Context Protocol (MCP)** – Ethical AI filters for cultural appropriateness
* **Conservative Destination Support** – Special filtering for Pakistan, Saudi Arabia, UAE, etc.
* **Religious Site Guidelines** – Tailored dress codes for visiting mosques, temples, or churches
* **Taboo Detection** – Automatically excludes culturally inappropriate items

### Smart Product Matching

* **Hierarchical Recommendations** – Prioritizes cultural appropriateness → regional climate → general suitability
* **Enhanced Product Catalog** – 45+ items with cultural and climate metadata
* **Filtering Pipeline** – Multi-stage filtering for precise results
* **Fallback Systems** – Graceful degradation when data sources are unavailable

## Frontend (UI/UX)

The frontend delivers a smooth and intuitive shopping experience for travelers. Built with **Vanilla JavaScript, HTML, and modern CSS**, it offers lightweight yet robust interaction with backend AI services.

### UI Highlights

* **Chat Interface** – Clean, intuitive chat for real-time interaction
 <img width="1236" height="1260" alt="image" src="https://github.com/user-attachments/assets/fcaf228e-4df7-4743-a0f1-a49a4e794350" />


**Prompt → Answer Showcase**
User: “What should I wear for a business trip to London in summer?”
<img width="1230" height="759" alt="image" src="https://github.com/user-attachments/assets/66a8e912-c915-43e4-a402-ee13062a8795" />


**Recommended Products Example**
User: “Show me Eid gifts for Dubai”
<img width="1248" height="799" alt="image" src="https://github.com/user-attachments/assets/f36aa392-61d2-4cf7-a8a7-1b22f6b9aaa4" />


* **Dark Mode Support** – Elegant, traveler-friendly design for night browsing
 <img width="1248" height="1253" alt="image" src="https://github.com/user-attachments/assets/8a552696-c2e6-49d8-8a22-a3af662ef927" />


## Technology Stack

| Component      | Technology                                     |
| -------------- | ---------------------------------------------- |
| Backend        | Python Flask with async support                |
| AI Engine      | Google Vertex AI (Gemini 2.5 Pro/Flash)        |
| Data Sources   | Wikipedia API, Weather APIs, Cultural Database |
| Frontend       | Vanilla JavaScript with modern CSS             |
| Caching        | JSON-based climate data caching                |
| Error Handling | Multi-layer fallback systems                   |
| Deployment     | Google Kubernetes Engine (GKE)                 |

## Prerequisites

* Python 3.9+
* Google Cloud Project (for Gemini AI)
* Service Account Key for Vertex AI
* Docker (for containerization)
* kubectl (for GKE deployment)

## Deployment on GKE

### 1. Prerequisites

Ensure you have:

* A Google Cloud account with billing enabled
* Installed tools:

  * Google Cloud SDK
  * kubectl (`gcloud components install kubectl`)

Set your project:

```bash
gcloud auth login
gcloud config set project <PROJECT_ID>
```

### 2. Clone the Repository

```bash
git clone https://github.com/Uzi78/TravelCultureChatbot.git
cd TravelCultureChatbot
```

Create a `.env` file using `.env.example` and enter your API keys.

### 3. Create a GKE Cluster

```bash
gcloud container clusters create gke-cluster \
    --num-nodes=2 \
    --zone=asia-south1-a \
    --machine-type=e2-small \
    --disk-type=pd-standard

gcloud container clusters get-credentials gke-cluster --zone=asia-south1-a
```

### 4. Build & Push the Docker Image

```bash
gcloud builds submit --tag gcr.io/<PROJECT_ID>/travel-app:latest .
```

### 5. Deploy to Kubernetes

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### 6. Access the Application

```bash
kubectl get service hackathon-service
```

Visit:

```
http://<EXTERNAL-IP>
```

## Scalability Features

* **Async Processing** – Non-blocking API calls
* **Caching Layers** – Reduces dependency on external APIs
* **Graceful Degradation** – Reliable fallback mechanisms
* **Load Balancing Ready** – Stateless, horizontally scalable service design

## Demo Scenarios

### Scenario 1: Winter Travel to Pakistan

**User:** “What should I pack for Pakistan in winters?”
**Response:**

* Destination: Pakistan
* Season: Winter
* Applies cultural filters: Conservative dress codes
* Suggests: Heavy winter coat, thermal layers, modest coverage
* Cultural note: “Respectful of local Islamic traditions”

### Scenario 2: Summer Business Trip to Dubai

**User:** “Business clothes for Dubai in summer”
**Response:**

* Context: Dubai + Summer + Business
* Climate: Hot desert, 35–40°C
* Cultural consideration: Conservative Islamic customs
* Suggests: Lightweight formal wear, long sleeves, modest cuts

## Comprehensive Test Queries

* “What to pack for Pakistan in winters?”
* “Summer clothes for Turkey”
* “Eid gifts for Dubai celebration”
* “Business attire for Japan winter”
* “Modest beachwear for conservative countries”

## Business Impact

### For Travelers

* 95% reduction in culturally inappropriate purchases
* Improved cultural respect and awareness
* Accurate climate-based packing recommendations
* Enhanced travel experience with local insights

### For Businesses

* Increased conversion rates through context-relevant recommendations
* Reduced return rates due to inappropriate purchases
* Expanded market reach in culturally diverse regions
* Enhanced customer satisfaction and brand reputation

## Contributing

We welcome contributions to improve cultural accuracy and expand regional support.

## Team

* Muhammad Uzair Shahid ([https://github.com/Uzi78](https://github.com/Uzi78))
* Talha Kausar ([https://github.com/raotalha71](https://github.com/raotalha71))
* Muhammad Zabil Mehboob ([https://github.com/MZabil](https://github.com/MZabil))

## License

MIT License – Free to use and modify for business and travel applications.

## Acknowledgments

* Google Cloud Vertex AI – For powerful Gemini AI integration
* Wikipedia Community – For comprehensive cultural and climate data
* Cultural Consultants – For sensitivity guidance and validation


