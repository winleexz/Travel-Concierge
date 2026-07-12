# Travel-Concierge
The Travel Concierge is a **multi-agent AI application built using LangChain, powered by Qwen-max LLM** for complex reasoning and planning to generate highly personalised travel plans. Through an intuitive web interface, users input their desired destination, travel dates, preferred star ratings, and travel styles (e.g., foodie, sightseeing).

The application utilizes a **Supervisor-Worker orchestration pattern** where a central Supervisor Agent coordinates three specialised sub-agents
1)	The Itinerary Planner dynamically adapts daily activities based on real-time weather forecasts (avoiding outdoor activities on rainy days) and calculates realistic geographical travel times to ensure itineraries are physically realistic

2)	The Hotel Recommender leverages live web search to find and filter accommodations based on real-time prices, ratings, and the user's specific travel style

3)	The Culinary Guide uses search API to pull authentic and highly-rated restaurant recommendations

Finally, the synthesized Markdown itinerary is seamlessly presented on screen and compiled into downloadable, professional .docx and .pptx documents for the user.

## App Architecture Diagram
Below is the visual flow and structural representation of how the components, sub-agents, and external tools are interacting within the application:

<img width="693" height="1179" alt="image" src="https://github.com/user-attachments/assets/3a09707d-8c5f-4dc0-a6bc-53ad640352d7" />

### Structural Breakdown of the Architecture:
1.	User Interface / Input Layer: Captures the user's destination, date range, and preferred travel style (e.g., relaxing, food-focused)

2.	Main Orchestrator: The central LangChain AgentExecutor that routes tasks to the appropriate specialized sub-agents
   
3.	Core AI Engine (Qwen-Max): The foundational Large Language Model responsible for understanding user intent, complex reasoning, and formatting the final output

4.	Sub-Agent 1: Itinerary Planner which focuses strictly on the day-by-day schedule. Use tools: get_current_date for baseline dates, get_weather_forecast to adapt activities to the weather, and get_travel_time_and_distance to ensure geographical logic and realistic transit times

5.	Sub-Agent 2: Hotel Recommender which focuses strictly on finding accommodations. Use tools: tavily_search_results to perform advanced, real-time web searches to find actual hotels, filtering them by star rating, price, and user style

6.	Sub-Agent 3: Culinary Guide which focuses strictly on finding food recommendations. Use tools: tavily_search_results to perform advanced, real-time web searches to find actual restaurants, filtering them by star rating

7.	External API Layer: The real-world data providers (Open-Meteo, OpenStreetMap/Nominatim, OSRM, and Tavily) that ground the LLM's hallucinations in factual, real-time data

8.	Output Layer: Combines the Markdown outputs from both sub-agents into a single, cohesive, and clean travel document for the user



