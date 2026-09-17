# Smart India Hackathon Workshop
# Date:17-09-2026
## Register Number:212224040097
## Name: HARESH R
## Problem Title
SIH 1710: Enhancing Navigation for Railway Station Facilities and Locations
## Problem Description
Background: Railway stations are complex environments with numerous facilities and locations such as ticket counters, platforms, restrooms, food courts, and waiting areas. Passengers often face difficulties in navigating these spaces, especially in large or unfamiliar stations. Efficient and user-friendly navigation systems are crucial for improving passenger experience, reducing congestion, and ensuring timely travel connections. Description: The problem involves developing a comprehensive navigation solution for railway stations that assists passengers in locating various facilities and destinations within the station premises. This includes creating detailed maps, providing real-time directions, and integrating features such as accessibility options for individuals with disabilities. The solution should be intuitive, easy to use, and accessible via multiple platforms, including mobile devices and digital kiosks. Key challenges include updating navigation information in real-time, ensuring accuracy, and accommodating the diverse needs of all passengers. Expected Solution: The expected solution is a multi-platform navigation system that provides detailed, real-time directions to all facilities and locations within a railway station. This system should include: A mobile application with 3D interactive maps and step-by-step navigation. Digital kiosks located throughout the station with touch-screen interfaces. Voice-guided navigation for visually impaired passengers. Regular updates to reflect changes in station layout and facility locations. Integration with existing railway apps and services for seamless user experience. The solution should enhance the overall passenger experience by reducing confusion, saving time, and improving accessibility within the station.

## Problem Creater's Organization
Ministry of Railway

## Idea
RailWayNav+ is a smart railway station navigation system that helps passengers easily find and reach facilities such as platforms, ticket counters, restrooms, food courts, waiting halls, lifts and parking areas.

It provides an interactive station map, facility search, step-by-step navigation, accessibility mode and voice guidance. The system can be used through mobile devices and digital kiosks.


## Proposed Solution / Architecture Diagram

Proposed Solution

RailWayNav+ provides a simple and accessible way to navigate inside railway stations.

Working:

Passenger → Search Facility → Select Destination → Route Calculation → Interactive Map → Step-by-Step / Voice Guidance → Destination

Architecture Diagram
              ┌─────────────────────┐
              │      Passenger      │
              └──────────┬──────────┘
                         ↓
        ┌────────────────────────────────┐
        │ Web / Mobile App / Digital     │
        │            Kiosk               │
        └───────────────┬────────────────┘
                        ↓
             ┌─────────────────────┐
             │    RailWayNav+      │
             │ Navigation System   │
             └──────────┬──────────┘
                        ↓
          ┌──────────────────────────┐
          │ Station Map & Facility  │
          │       Information       │
          └────────────┬─────────────┘
                       ↓
             ┌──────────────────┐
             │ Route Calculation│
             └────────┬─────────┘
                      ↓
       ┌──────────────────────────────┐
       │ Map Route + Voice Guidance   │
       │ + Accessibility Support      │
       └──────────────┬───────────────┘
                      ↓
              ┌──────────────┐
              │ Destination  │
              └──────────────┘
              
## Use Cases
1. Passenger
Search for station facilities.
View the station map.
Select a destination.
Get step-by-step directions.
Find platforms, restrooms, ticket counters and food courts.
2. Visually Impaired Passenger
Enable voice guidance.
Receive audio navigation instructions.
Find important facilities using voice assistance.
3. Passenger with Disability
Enable accessibility mode.
Find lifts and accessible facilities.
Follow step-free routes.
4. Railway Staff / Admin
Update facility locations.
Update station layout information.
Maintain navigation data.
5. Digital Kiosk User
Search facilities using a touchscreen.
View the station map.
Get directions to the selected location.

## Technology Stack
Technology	Purpose
React.js	Frontend and user interface
JavaScript	Application functionality
HTML5	Page structure
CSS3	Design and responsive layout
Vite	Development and build tool
Web Speech API	Voice guidance
Git & GitHub	Version control and project hosting

## Dependencies
```
Node.js
npm
React
React DOM
Vite
Web Speech API
Modern Web Browser
Git
GitHub
```
## Program
```
import { useState } from "react";
import "./App.css";

const facilities = [
  {
    id: 1,
    name: "Platform 1",
    icon: "🚉",
    category: "Platform",
    floor: "Ground Floor",
    distance: "120 m",
    time: "2 min",
  },
  {
    id: 2,
    name: "Platform 2",
    icon: "🚉",
    category: "Platform",
    floor: "Ground Floor",
    distance: "180 m",
    time: "3 min",
  },
  {
    id: 3,
    name: "Ticket Counter",
    icon: "🎫",
    category: "Ticket",
    floor: "Ground Floor",
    distance: "80 m",
    time: "1 min",
  },
  {
    id: 4,
    name: "Restroom",
    icon: "🚻",
    category: "Restroom",
    floor: "Ground Floor",
    distance: "60 m",
    time: "1 min",
  },
  {
    id: 5,
    name: "Food Court",
    icon: "🍴",
    category: "Food",
    floor: "First Floor",
    distance: "150 m",
    time: "3 min",
  },
  {
    id: 6,
    name: "Waiting Hall",
    icon: "🪑",
    category: "Waiting",
    floor: "Ground Floor",
    distance: "100 m",
    time: "2 min",
  },
  {
    id: 7,
    name: "Lift",
    icon: "🛗",
    category: "Accessibility",
    floor: "All Floors",
    distance: "50 m",
    time: "1 min",
  },
  {
    id: 8,
    name: "Parking Area",
    icon: "🅿️",
    category: "Parking",
    floor: "Outside",
    distance: "200 m",
    time: "4 min",
  },
];

function App() {
  const [search, setSearch] = useState("");
  const [selectedFacility, setSelectedFacility] = useState(null);
  const [accessibleMode, setAccessibleMode] = useState(false);
  const [voiceMode, setVoiceMode] = useState(false);
  const [activeCategory, setActiveCategory] = useState("All");

  const categories = [
    "All",
    "Platform",
    "Ticket",
    "Restroom",
    "Food",
    "Waiting",
    "Accessibility",
  ];

  const filteredFacilities = facilities.filter((facility) => {
    const matchesSearch =
      facility.name.toLowerCase().includes(search.toLowerCase());

    const matchesCategory =
      activeCategory === "All" ||
      facility.category === activeCategory;

    return matchesSearch && matchesCategory;
  });

  const startNavigation = (facility) => {
    setSelectedFacility(facility);

    if (voiceMode && "speechSynthesis" in window) {
      const message = new SpeechSynthesisUtterance(
        `Navigation started to ${facility.name}. Distance ${facility.distance}. Estimated time ${facility.time}.`
      );

      window.speechSynthesis.speak(message);
    }

    window.scrollTo({
      top: 180,
      behavior: "smooth",
    });
  };

  const useVoiceGuidance = () => {
    setVoiceMode(!voiceMode);

    if (!voiceMode && "speechSynthesis" in window) {
      const message = new SpeechSynthesisUtterance(
        "Voice guidance enabled. Search for a facility to begin navigation."
      );

      window.speechSynthesis.speak(message);
    }
  };

  return (
    <div className="app">

      {/* HEADER */}
      <header className="header">
        <div className="logo-section">
          <div className="logo">🚆</div>

          <div>
            <h1>RailWayNav+</h1>
            <p>Smart Railway Station Navigation</p>
          </div>
        </div>

        <div className="header-buttons">
          <button
            className={accessibleMode ? "header-btn active" : "header-btn"}
            onClick={() => setAccessibleMode(!accessibleMode)}
          >
            ♿ Accessibility
          </button>

          <button
            className={voiceMode ? "header-btn active" : "header-btn"}
            onClick={useVoiceGuidance}
          >
            🔊 Voice Guide
          </button>
        </div>
      </header>

      {/* HERO */}
      <section className="hero">
        <div className="hero-content">
          <div className="hero-text">
            <span className="badge">SIH 1710</span>

            <h2>
              Navigate Railway Stations
              <span> Easily & Safely</span>
            </h2>

            <p>
              Find platforms, ticket counters, restrooms, food courts,
              waiting halls and other station facilities with simple
              step-by-step navigation.
            </p>

            <div className="hero-buttons">
              <button
                className="primary-btn"
                onClick={() =>
                  document
                    .getElementById("facilities")
                    .scrollIntoView({ behavior: "smooth" })
                }
              >
                🧭 Find a Facility
              </button>

              <button
                className="secondary-btn"
                onClick={() =>
                  document
                    .getElementById("map")
                    .scrollIntoView({ behavior: "smooth" })
                }
              >
                🗺️ View Station Map
              </button>
            </div>
          </div>

          <div className="hero-card">
            <div className="train-icon">🚆</div>
            <h3>Station Navigation</h3>
            <p>Simple • Fast • Accessible</p>

            <div className="mini-stats">
              <div>
                <strong>8+</strong>
                <small>Facilities</small>
              </div>

              <div>
                <strong>3D</strong>
                <small>Map Ready</small>
              </div>

              <div>
                <strong>24/7</strong>
                <small>Access</small>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* SEARCH */}
      <section className="search-area" id="facilities">
        <div className="section-heading">
          <span>📍</span>
          <div>
            <h2>Find a Facility</h2>
            <p>Search for your destination inside the station</p>
          </div>
        </div>

        <div className="search-box">
          <span>🔍</span>

          <input
            type="text"
            placeholder="Search platform, restroom, food court..."
            value={search}
            onChange={(e) => setSearch(e.target.value)}
          />

          {search && (
            <button onClick={() => setSearch("")}>✕</button>
          )}
        </div>

        <div className="category-list">
          {categories.map((category) => (
            <button
              key={category}
              className={
                activeCategory === category
                  ? "category active-category"
                  : "category"
              }
              onClick={() => setActiveCategory(category)}
            >
              {category}
            </button>
          ))}
        </div>
      </section>

      {/* NAVIGATION RESULT */}
      {selectedFacility && (
        <section className="navigation-result">
          <div className="navigation-left">
            <div className="navigation-icon">
              {selectedFacility.icon}
            </div>

            <div>
              <span className="navigation-label">
                NAVIGATION STARTED
              </span>

              <h2>{selectedFacility.name}</h2>

              <p>
                Follow the blue route to reach your destination.
              </p>

              <div className="route-info">
                <span>📏 {selectedFacility.distance}</span>
                <span>⏱ {selectedFacility.time}</span>
                <span>📍 {selectedFacility.floor}</span>
              </div>

              {accessibleMode && (
                <div className="accessible-route">
                  ♿ Accessible route enabled — lifts and
                  step-free paths are preferred.
                </div>
              )}
            </div>
          </div>

          <button
            className="close-navigation"
            onClick={() => setSelectedFacility(null)}
          >
            Stop Navigation
          </button>
        </section>
      )}

      {/* MAP */}
      <section className="map-section" id="map">
        <div className="section-heading">
          <span>🗺️</span>
          <div>
            <h2>Interactive Station Map</h2>
            <p>Visualize important locations inside the station</p>
          </div>
        </div>

        <div className="station-map">

          <div className="map-road road-one"></div>
          <div className="map-road road-two"></div>
          <div className="map-road road-three"></div>

          <div className="map-building main-building">
            <strong>🏢 MAIN STATION</strong>
            <small>Ground Floor</small>
          </div>

          <button
            className="map-location entrance-location"
            onClick={() => startNavigation(facilities[2])}
          >
            🚪
            <span>Main Entrance</span>
          </button>

          <button
            className="map-location ticket-location"
            onClick={() => startNavigation(facilities[2])}
          >
            🎫
            <span>Ticket Counter</span>
          </button>

          <button
            className="map-location waiting-location"
            onClick={() => startNavigation(facilities[5])}
          >
            🪑
            <span>Waiting Hall</span>
          </button>

          <button
            className="map-location food-location"
            onClick={() => startNavigation(facilities[4])}
          >
            🍴
            <span>Food Court</span>
          </button>

          <button
            className="map-location restroom-location"
            onClick={() => startNavigation(facilities[3])}
          >
            🚻
            <span>Restroom</span>
          </button>

          <button
            className="map-location lift-location"
            onClick={() => startNavigation(facilities[6])}
          >
            🛗
            <span>Lift</span>
          </button>

          <div className="platform platform-one">
            <span>🚉</span>
            <strong>PLATFORM 1</strong>
          </div>

          <div className="platform platform-two">
            <span>🚉</span>
            <strong>PLATFORM 2</strong>
          </div>

          <div className="current-location">
            <div className="location-dot"></div>
            <span>You are here</span>
          </div>

          {selectedFacility && (
            <div className="map-route">
              <span>🧭 Route to {selectedFacility.name}</span>
            </div>
          )}

        </div>

        <div className="map-legend">
          <span>
            <i className="blue-dot"></i>
            Your Location
          </span>

          <span>
            <i className="green-dot"></i>
            Facility
          </span>

          <span>
            <i className="yellow-dot"></i>
            Platform
          </span>

          <span>
            <i className="red-dot"></i>
            Entrance
          </span>
        </div>
      </section>

      {/* FACILITY CARDS */}
      <section className="facility-section">
        <div className="section-title-row">
          <div>
            <h2>📍 Station Facilities</h2>
            <p>Select a destination to start navigation</p>
          </div>

          <span className="facility-count">
            {filteredFacilities.length} Facilities
          </span>
        </div>

        <div className="facility-grid">
          {filteredFacilities.map((facility) => (
            <div className="facility-card" key={facility.id}>

              <div className="facility-top">
                <div className="facility-icon">
                  {facility.icon}
                </div>

                <span className="distance">
                  {facility.distance}
                </span>
              </div>

              <h3>{facility.name}</h3>

              <p>
                📍 {facility.floor}
              </p>

              <div className="card-bottom">
                <span>⏱ {facility.time}</span>

                <button
                  onClick={() => startNavigation(facility)}
                >
                  Navigate →
                </button>
              </div>
            </div>
          ))}
        </div>

        {filteredFacilities.length === 0 && (
          <div className="no-results">
            <div>🔎</div>
            <h3>No facility found</h3>
            <p>Try searching for another facility.</p>
          </div>
        )}
      </section>

      {/* FEATURES */}
      <section className="features-section">
        <div className="section-heading center-heading">
          <span>✨</span>
          <div>
            <h2>Smart Navigation Features</h2>
            <p>Designed for every railway passenger</p>
          </div>
        </div>

        <div className="features-grid">

          <div className="feature-card">
            <div className="feature-icon">🗺️</div>
            <h3>Interactive Maps</h3>
            <p>
              Easy-to-understand digital maps help passengers
              locate facilities quickly.
            </p>
          </div>

          <div className="feature-card">
            <div className="feature-icon">🧭</div>
            <h3>Step-by-Step Navigation</h3>
            <p>
              Clear directions guide passengers from their
              current location to the destination.
            </p>
          </div>

          <div className="feature-card">
            <div className="feature-icon">♿</div>
            <h3>Accessibility Mode</h3>
            <p>
              Accessible routes can prioritize lifts and
              step-free paths.
            </p>
          </div>

          <div className="feature-card">
            <div className="feature-icon">🔊</div>
            <h3>Voice Guidance</h3>
            <p>
              Voice instructions help visually impaired
              passengers navigate the station.
            </p>
          </div>

          <div className="feature-card">
            <div className="feature-icon">🔄</div>
            <h3>Real-Time Updates</h3>
            <p>
              Station information can be updated when layouts
              or facility locations change.
            </p>
          </div>

          <div className="feature-card">
            <div className="feature-icon">📱</div>
            <h3>Multi-Platform</h3>
            <p>
              The system can be extended to mobile applications
              and digital railway kiosks.
            </p>
          </div>

        </div>
      </section>

      {/* HOW IT WORKS */}
      <section className="how-section">
        <div className="section-heading center-heading">
          <span>⚡</span>
          <div>
            <h2>How RailWayNav+ Works</h2>
            <p>Navigate in four simple steps</p>
          </div>
        </div>

        <div className="steps-grid">

          <div className="step">
            <div className="step-number">01</div>
            <h3>Search</h3>
            <p>Search for the facility you need.</p>
          </div>

          <div className="step">
            <div className="step-number">02</div>
            <h3>Select</h3>
            <p>Select your destination from the list.</p>
          </div>

          <div className="step">
            <div className="step-number">03</div>
            <h3>Navigate</h3>
            <p>Follow the route shown on the station map.</p>
          </div>

          <div className="step">
            <div className="step-number">04</div>
            <h3>Reach</h3>
            <p>Reach your destination safely and easily.</p>
          </div>

        </div>
      </section>

      {/* FOOTER */}
      <footer>
        <div className="footer-content">
          <div>
            <h2>🚆 RailWayNav+</h2>
            <p>
              Enhancing Navigation for Railway Station
              Facilities and Locations
            </p>
          </div>

          <div className="footer-info">
            <span>SIH 1710</span>
            <span>Ministry of Railways</span>
            <span>Smart • Accessible • User Friendly</span>
          </div>
        </div>

        <div className="copyright">
          © 2026 RailWayNav+ | Smart India Hackathon Solution
        </div>
      </footer>

    </div>
  );
}

export default App;
```

## output

<img width="1876" height="993" alt="Screenshot 2026-09-17 223702" src="https://github.com/user-attachments/assets/973e9d74-028b-448e-97d9-f652f88d905e" />
<img width="1847" height="847" alt="Screenshot 2026-09-17 223727" src="https://github.com/user-attachments/assets/bb65c0c1-4c94-4f11-b2a8-2a36d739d64d" />
<img width="1821" height="788" alt="Screenshot 2026-09-17 223749" src="https://github.com/user-attachments/assets/93322ccc-0ae5-495f-8cee-e297f497c533" />
<img width="1706" height="800" alt="Screenshot 2026-09-17 223805" src="https://github.com/user-attachments/assets/5bc154e5-1fc0-4acc-9611-6abca66f3f35" />
<img width="1752" height="746" alt="Screenshot 2026-09-17 223826" src="https://github.com/user-attachments/assets/b2b91cb6-a49c-48af-8ca1-4127f67eb078" />

## result

Thus, the RailWayNav+ railway station navigation system was successfully developed using React.js. The system allows users to search and locate railway station facilities, view an interactive station map, navigate to destinations, and use accessibility and voice guidance features.
