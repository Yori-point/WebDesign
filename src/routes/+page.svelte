<script>
  /** @typedef {Object} Place
   * @property {string} name
   * @property {string} map
   */

  /** @typedef {Object} City
   * @property {string} id
   * @property {string} name
   * @property {string} note
   * @property {Place[]} places
   */

  /** @typedef {Object} Country
   * @property {string} id
   * @property {string} name
   * @property {string} flag
   * @property {string} image
   * @property {City[]} cities
   */

  /** @type {City | null} */
  let selectedCity = $state(null);

  /** @type {Country | null} */
  let selectedCountry = $state(null);

  // To add a new place, add a new object inside the places array of a city.
  /** @type {Country[]} */
  const countries = [
    {
      id: 'italy',
      name: 'Italy',
      flag: '🇮🇹',
      image: '/images/Italy.png',
      cities: [
        {
          id: 'milan',
          name: 'Milan',
          note: 'A place that taught me how to begin again, even on days when I did not feel brave.',
          places: [
            { name: 'Duomo di Milano', map: 'https://www.google.com/maps/search/?api=1&query=Duomo+di+Milan' },
            { name: 'La Scala', map: 'https://www.google.com/maps/search/?api=1&query=La+Scala+Milan' }
          ]
        },
        {
          id: 'florence',
          name: 'Florence',
          note: 'Beauty was everywhere, almost too complete, like a painting I was afraid to disturb.',
          places: [
            { name: 'Cattedrale di Santa Maria del Fiore', map: 'https://www.google.com/maps/search/?api=1&query=Cattedrale+di+Santa+Maria+del+Fiore+Florence' },
            { name: 'Galleria degli Uffizi', map: 'https://www.google.com/maps/search/?api=1&query=Galleria+degli+Uffizi+Florence' },
            { name: 'Piazzale Michelangelo', map: 'https://www.google.com/maps/search/?api=1&query=Piazzale+Michelangelo+Florence' },
            { name: 'Scalinata di Trinità dei Monti', map: 'https://maps.app.goo.gl/42xjZzDtsfU4f7iJ6' }
          ]
        },
        {
          id: 'turin',
          name: 'Turin',
          note: 'Quiet, restrained, and elegant, as if the city keeps its best thoughts behind closed doors.',
          places: [
            { name: 'Palazzo Reale di Torino', map: 'https://www.google.com/maps/search/?api=1&query=Palazzo+Reale+di+Torino' },
            { name: 'Castello del Valentino', map: 'https://www.google.com/maps/search/?api=1&query=Castello+del+Valentino+Turin' },
            { name: 'Museo Egizio', map: 'https://www.google.com/maps/search/?api=1&query=Museo+Egizio+Turin' },
            { name: 'Scalinata di Trinità dei Monti', map: 'https://maps.app.goo.gl/42xjZzDtsfU4f7iJ6' }
          ]
        },
        {
          id: 'como',
          name: 'Como',
          note: 'A soft breath between water and mountains, where time seemed to loosen its grip.',
          places: [
            { name: 'Duomo di Como', map: 'https://www.google.com/maps/search/?api=1&query=Duomo+Como' },
            { name: 'Lago di Como', map: 'https://www.google.com/maps/search/?api=1&query=Lago+di+Como' }
          ]
        },
        {
          id: 'rome',
          name: 'Rome',
          note: 'Ruins, noise, sunlight, and life, all speaking at once.',
          places: [
            { name: 'Colosseum', map: 'https://www.google.com/maps/search/?api=1&query=Colosseum+Rome' },
            { name: 'Vatican City', map: 'https://www.google.com/maps/search/?api=1&query=Vatican+City' },
            { name: 'Trevi Fountain', map: 'https://www.google.com/maps/search/?api=1&query=Trevi+Fountain+Rome' },
            { name: 'Scalinata di Trinità dei Monti', map: 'https://www.google.com/maps/search/?api=1&query=Scalinata+di+Trinità+dei+Monti+Rome' }
          ]
        },
        {
          id: 'siena',
          name: 'Siena',
          note: 'A gentle afternoon held me there, and for a moment, being alone felt light.',
          places: [
            { name: 'Piazza del Campo', map: 'https://www.google.com/maps/search/?api=1&query=Piazza+del+Campo+Siena' },
            { name: 'Pinacoteca Nazionale di Siena', map: 'https://www.google.com/maps/search/?api=1&query=Pinacoteca+Nazionale+di+Siena' },
            { name: 'Palazzo Salimbeni', map: 'https://www.google.com/maps/search/?api=1&query=Palazzo+Salimbeni+Siena' }
          ]
        },
        {
          id: 'pisa',
          name: 'Pisa',
          note: 'A small postcard of wonder, simple enough to remember without effort.',
          places: [
            { name: 'Torre di Pisa', map: 'https://www.google.com/maps/search/?api=1&query=Torre+di+Pisa' }
          ]
        },
        {
          id: 'cinque terre',
          name: 'Cinque Terre',
          note: 'Colors leaning toward the sea, as if the houses were trying to stay inside summer.',
          places: [
            { name: 'Monterosso al Mare', map: 'https://www.google.com/maps/search/?api=1&query=Monterosso+al+Mare' },
            { name: 'Castello di Vernazza', map: 'https://www.google.com/maps/search/?api=1&query=Castello+di+Vernazza' },
            { name: 'Corniglia', map: 'https://www.google.com/maps/search/?api=1&query=Corniglia' },
            { name: 'Manarola', map: 'https://www.google.com/maps/search/?api=1&query=Manarola' },
            { name: 'Riomaggiore', map: 'https://www.google.com/maps/search/?api=1&query=Riomaggiore' }
          ]
        }
      ]
    },
    {
      id: 'france',
      name: 'France',
      flag: '🇫🇷',
      image: '/images/France.png',
      cities: [
        {
          id: 'paris',
          name: 'Paris',
          note: 'A city made of cinema, books, and small heartbreaks, still beautiful even when it refuses to be easy.',
          places: [
            { name: 'Eiffel Tower', map: 'https://www.google.com/maps/search/?api=1&query=Eiffel+Tower+Paris' },
            { name: 'Orsay Museum', map: 'https://www.google.com/maps/search/?api=1&query=Musée+d%27Orsay+Paris' },
            { name: 'Louvre Museum', map: 'https://www.google.com/maps/search/?api=1&query=Louvre+Museum+Paris' },
            { name: 'Orangerie Museum', map: 'https://www.google.com/maps/search/?api=1&query=Musée+de+l%27Orangerie+Paris' },
            { name: 'Place de la Bastille', map: 'https://www.google.com/maps/search/?api=1&query=Place+de+la+Bastille+Paris' },
            { name: 'Pompidou Centre', map: 'https://www.google.com/maps/search/?api=1&query=Le+Centre+Pompidou+Paris' }
          ]
        },
        {
          id: 'nice',
          name: 'Nice',
          note: 'Sunlight, blue water, and a brightness that made everything feel briefly easier.',
          places: [
            { name: 'SAB Blue Chair', map: 'https://www.google.com/maps/search/?api=1&query=SAB+Blue+Chair+Nice' },
            { name: 'Vieille Ville', map: 'https://www.google.com/maps/search/?api=1&query=Vieille+Ville+Nice' },
            { name: 'Cours Saleya', map: 'https://www.google.com/maps/search/?api=1&query=Cours+Saleya+Nice' },
            { name: 'Place Masséna', map: 'https://www.google.com/maps/search/?api=1&query=Place+Masséna+Nice' }
          ]
        },
        {
          id: 'antibes',
          name: 'Antibes',
          note: 'A quieter blue, with old stones, sea wind, and the softness of a place that does not ask for attention.',
          places: [
            { name: 'St. Andrew Bastion', map: 'https://www.google.com/maps/search/?api=1&query=St.+Andrew+Bastion+Antibes' },
            { name: 'Point de vue pointe de l&#39;Îlette', map: 'https://www.google.com/maps/search/?api=1&query=Point+de+vue+pointe+de+l%27Îlette+Antibes' }
          ]
        }
      ]
    },
    {
      id: 'hungary',
      name: 'Hungary',
      flag: '🇭🇺',
      image: '/images/Hungary.png',
      cities: [
        {
          id: 'budapest',
          name: 'Budapest',
          note: 'Night lights on the river, old bridges, and a sadness that knows how to be romantic.',
          places: [
            { name: 'Parliament Building', map: 'https://www.google.com/maps/search/?api=1&query=Parliament+Building+Budapest' },
            { name: 'Buda Castle', map: 'https://www.google.com/maps/search/?api=1&query=Buda+Castle+Budapest' },
            { name: 'Nagycsarnok', map: 'https://www.google.com/maps/search/?api=1&query=Nagycsarnok+Budapest' },
            { name: 'Liberty Bridge', map: 'https://www.google.com/maps/search/?api=1&query=Liberty+Bridge+Budapest' }
          ]
        }
      ]
    },
    {
      id: 'germany',
      name: 'Germany',
      flag: '🇩🇪',
      image: '/images/Germany.png',
      cities: [
        {
          id: 'munich',
          name: 'Munich',
          note: 'A city of Bavarian culture, museums, gardens and lively streets.',
          places: [
            { name: 'St. Peter', map: 'https://www.google.com/maps/search/?api=1&query=St.+Peter+Munich' },
            { name: 'Marienplatz', map: 'https://www.google.com/maps/search/?api=1&query=Marienplatz+Munich' },
            { name: 'Viktualienmarkt', map: 'https://www.google.com/maps/search/?api=1&query=Viktualienmarkt+Munich' },
            { name: 'Deutsches Museum', map: 'https://www.google.com/maps/search/?api=1&query=Deutsches+Museum+Munich' }
          ]
        },
        {
          id: 'nuremberg',
          name: 'Nuremberg',
          note: 'A fairytale surface, with history sleeping heavily underneath.',
          places: [
            { name: 'Nuremberg Castle', map: 'https://www.google.com/maps/search/?api=1&query=Nuremberg+Castle+Nuremberg' },
            { name: 'Toy Museum', map: 'https://www.google.com/maps/search/?api=1&query=Toy+Museum+Nuremberg' },
            { name: 'Maxbrücke', map: 'https://www.google.com/maps/search/?api=1&query=Maxbrücke+Nuremberg' }
          ]
        }
      ]
    },
    {
      id: 'switzerland',
      name: 'Switzerland',
      flag: '🇨🇭',
      image: '/images/Switzerland.png',
      cities: [
        {
          id: 'locarno',
          name: 'Locarno',
          note: 'Lake light, quiet streets, and a southern softness under a Swiss sky.',
          places: [
            { name: 'Piazza Grande', map: 'https://www.google.com/maps/search/?api=1&query=Piazza+Grande+Locarno' },
            { name: 'Castello Visconteo', map: 'https://www.google.com/maps/search/?api=1&query=Castello+Visconteo+Locarno' }
          ]
        }
      ]
    },
    {
      id: 'austria',
      name: 'Austria',
      flag: '🇦🇹',
      image: '/images/Austria.png',
      cities: [
        {
          id: 'vienna',
          name: 'Vienna',
          note: 'Music seemed to stay in the walls, even after everyone had left.',
          places: [
            { name: 'Schönbrunn Palace', map: 'https://www.google.com/maps/search/?api=1&query=Schönbrunn+Palace+Vienna' },
            { name: 'St. Stephen\'s Cathedral', map: 'https://www.google.com/maps/search/?api=1&query=St.+Stephen%27s+Cathedral+Vienna' },
            { name: 'Natural History Museum', map: 'https://www.google.com/maps/search/?api=1&query=Natural+History+Museum+Vienna' },
            { name: 'Pathological-anatomical collection in the Narrenturm', map: 'https://www.google.com/maps/search/?api=1&query=Pathological-anatomical+collection+in+the+Narrenturm+Vienna' }
          ]
        }
      ]
    },
    {
      id: 'belgium',
      name: 'Belgium',
      flag: '🇧🇪',
      image: '/images/Belgium.png',
      cities: [
        {
          id: 'brussels',
          name: 'Brussels',
          note: 'Chocolate, rain, paper notes, and feelings I did not know where to put.',
          places: [
            { name: 'Grand-Place', map: 'https://www.google.com/maps/search/?api=1&query=Grand-Place+Brussels' },
            { name: 'Atomium', map: 'https://www.google.com/maps/search/?api=1&query=Atomium+Brussels' },
            { name: 'European Parliament', map: 'https://www.google.com/maps/search/?api=1&query=European+Parliament+Brussels' },
            { name: 'Sewer Museum', map: 'https://www.google.com/maps/search/?api=1&query=Sewer+Museum+Brussels' }
          ]
        },
        {
          id: 'gent',
          name: 'Gent',
          note: 'Old canals, soft brick walls, and a quiet beauty that feels less displayed than simply lived.',
          places: [
            { name: 'Sint-Niklaaskerk', map: 'https://www.google.com/maps/search/?api=1&query=Sint-Niklaaskerk+Gent' },
            { name: 'Beeld van Oswald de Kerchove de Denterghem', map: 'https://www.google.com/maps/search/?api=1&query=Beeld+van+Oswald+de+Kerchove+de+Denterghem+Gent' }
          ]
        },
        {
          id: 'leuven',
          name: 'Leuven',
          note: 'Young streets, low voices, and the strange hope that something could still begin.',
          places: [
            { name: 'St. Peter\'s Church', map: 'https://www.google.com/maps/search/?api=1&query=St.+Peter%27s+Church+Leuven' },
            { name: 'University library and library tower', map: 'https://www.google.com/maps/search/?api=1&query=University+library+and+library+tower+Leuven' }
          ]
        }
      ]
    },
    {
      id: 'estonia',
      name: 'Estonia',
      flag: '🇪🇪',
      image: '/images/Estonia.png',
      cities: [
        {
          id: 'tallinn',
          name: 'Tallinn',
          note: 'Medieval charm in the Baltics, and a kind of northern magic that speaks very softly.',
          places: [
            { name: 'Old Town', map: 'https://www.google.com/maps/search/?api=1&query=Old+Town+Tallinn' },
            { name: 'Kadriorg Park', map: 'https://www.google.com/maps/search/?api=1&query=Kadriorg+Park+Tallinn' }
          ]
        }
      ]
    },
    {
      id: 'romania',
      name: 'Romania',
      flag: '🇷🇴',
      image: '/images/Romania.png',
      cities: [
        {
          id: 'bucharest',
          name: 'Bucharest',
          note: 'Unpolished, restless, and alive, with beauty hiding in rough corners.',
          places: [
            { name: 'Romanian Athenaeum', map: 'https://www.google.com/maps/search/?api=1&query=Romanian+Athenaeum+Bucharest' },
            { name: 'Museum of Communism in Bucharest', map: 'https://www.google.com/maps/search/?api=1&query=Museum+of+Communism+in+Bucharest' },
            { name: 'The Umbrellas\' Street', map: 'https://www.google.com/maps/search/?api=1&query=The+Umbrellas+Street+Bucharest' }
          ]
        },
        {
          id: 'sibiu',
          name: 'Sibiu',
          note: 'Little eyes on the roofs, watching time pass without saying anything.',
          places: [
            { name: 'Piața Mare', map: 'https://www.google.com/maps/search/?api=1&query=Piața+Mare+Sibiu' },
            { name: 'Council Tower', map: 'https://www.google.com/maps/search/?api=1&query=Council+Tower+Sibiu' },
            { name: 'Podul Minciunilor', map: 'https://www.google.com/maps/search/?api=1&query=Podul+Minciunilor+Sibiu' }
          ]
        },
        {
          id: 'brasov',
          name: 'Brașov',
          note: 'Mountains around the streets, like a darker fairytale waiting behind the windows.',
          places: [
            { name: 'Black Church', map: 'https://www.google.com/maps/search/?api=1&query=Black+Church+Brașov' },
            { name: 'Council Square', map: 'https://www.google.com/maps/search/?api=1&query=Council+Square+Brașov' }
          ]
        },
        {
          id: 'cluj-napoca',
          name: 'Cluj-Napoca',
          note: 'A lived-in city, young and practical, with no need to perform charm.',
          places: [
            { name: 'Old Town', map: 'https://www.google.com/maps/search/?api=1&query=Old+Town+Cluj-Napoca' }
          ]
        },
      ]
    },
    {
      id: 'finland',
      name: 'Finland',
      flag: '🇫🇮',
      image: '/images/Finland.png',
      cities: [
        {
          id: 'helsinki',
          name: 'Helsinki',
          note: 'A pale, quiet city where silence felt clean rather than empty.',
          places: [
            { name: 'Suomenlinna', map: 'https://www.google.com/maps/search/?api=1&query=Suomenlinna+Helsinki' },
            { name: 'Design Museum', map: 'https://www.google.com/maps/search/?api=1&query=Design+Museum+Helsinki' }
          ]
        }
      ]
    }
  ];

  // Helper functions
  function getTotalCities() {
    return countries.reduce((sum, country) => sum + country.cities.length, 0);
  }

  function getTotalPlaces() {
    return countries.reduce((sum, country) => sum + country.cities.reduce((citySum, city) => citySum + city.places.length, 0), 0);
  }

  /** @param {City} city @param {Country} country */
  function selectCity(city, country) {
    selectedCity = city;
    selectedCountry = country;
  }

  function backToCities() {
    selectedCity = null;
    selectedCountry = null;
  }
</script>

<main class="page">
  <section class="hero" id="hero">
    <div class="hero-top">
      <div class="logo">Yori</div>
      <nav>
        <a href="https://www.instagram.com/tramonto0.7?igsh=eWtycDRkaGE2cjlp&utm_source=qr" target="_blank" rel="noreferrer">
            About
        </a>
        <a href="https://www.instagram.com/webdesign_ddc" target="_blank" rel="noreferrer">
            @webdesign_ddc
        </a>
    </nav>
    </div>
    <div class="hero-inner">
      <div class="hero-left">
        <h1>I have to leave, I have to travel, my heart should go to freedom.</h1>
        <p class="intro-text">
          A personal archive of places I have been, cities I have walked through, and small memories collected along the way.
        </p>
      </div>

      <div class="hero-right">
        <div class="stats-grid">
          <a href="#countries" class="stat-card">
            <strong>{countries.length}</strong>
            <span>countries</span>
          </a>
          <a href="#cities" class="stat-card">
            <strong>{getTotalCities()}</strong>
            <span>cities</span>
          </a>
          <div class="stat-card">
            <strong>{getTotalPlaces()}</strong>
            <span>places</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section class="country-overview" id="countries">
    <div class="section-header">
      <p class="section-label">Browse by country</p>
      <h2>Choose a country, start exploring my journey</h2>
    </div>

    <div class="country-grid">
      {#each countries as country}
        <a href="#cities-{country.id}" class="country-card">
          <div class="country-card-top">
            <img src={country.image} alt={country.name} class="country-image" />
            <div>
              <strong>{country.name}</strong>
              <p>{country.cities.length} cities · {country.cities.reduce((sum, city) => sum + city.places.length, 0)} places</p>
            </div>
          </div>
          <p class="country-cities">{country.cities.map(c => c.name).join(' · ')}</p>
        </a>
      {/each}
    </div>
  </section>
  <section id="cities">
    <div class="cities-container">
      <div class="section-header">
        <p class="section-label">Explore cities</p>
        <h2>All cities, choose one to start exploring</h2>
      </div>
      {#each countries as country}
        <div class="country-block" id="cities-{country.id}">
          <h3>{country.name}</h3>
          <div class="city-grid">
            {#each country.cities as city}
              <button type="button" class="city-card" onclick={() => selectCity(city, country)}>
                <strong>{city.name}</strong>
              </button>
            {/each}
          </div>
          {#if selectedCity && selectedCountry && selectedCountry.id === country.id}
            <section class="city-detail">
              <button type="button" onclick={backToCities}>Close</button>
              <h2>{selectedCity.name}</h2>
              <p>{selectedCountry.name}</p>
              <p>{selectedCity.note}</p>
              <div class="places-chips">
                {#each selectedCity.places as place}
                  <a href={place.map} target="_blank" rel="noreferrer" class="place-chip">{place.name}</a>
                {/each}
              </div>
            </section>
          {/if}
        </div>
      {/each}
    </div>
  </section>

  <footer>
    <div class="footer-content">
      <div class="footer-main">
        <p>Yunwei Zhang</p>
      </div>
      <div class="footer-credit">
        <p>Web Design 2026</p>
        <p>Politecnico di Milano</p>
      </div>
    </div>
  </footer>
</main>

<style>
  :global(html) {
    scroll-behavior: smooth;
  }

  :global(body) {
    margin: 0;
    min-height: 100vh;
    background: #f5f5f0;
    color: #1b1f1a;
    font-family: Inter, system-ui, sans-serif;
  }

  :global(*) {
    box-sizing: border-box;
  }

  .page {
    min-height: 100vh;
  }

  .hero {
    min-height: 70vh;
    padding: 40px 36px;
    display: flex;
    flex-direction: column;
  }

  .hero-top {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 24px;
    margin-bottom: 48px;
  }

  nav {
    display: flex;
    gap: 24px;
    align-items: center;
  }

  nav a {
    color: #1b1f1a;
    text-decoration: none;
    font-size: 1rem;
    font-weight: 600;
  }

  nav a:hover {
    color: #6f9b63;
  }

  .hero-inner {
  width: min(100% - 48px, 1080px);
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 220px;
  gap: 80px;
  align-items: start;
  }

  .hero-left {
    display: flex;
    flex-direction: column;
    gap: 24px;
  }

  .hero-right {
  justify-self: end;
  }

  .logo {
  font-size: 1rem;
  font-weight: 600;
  letter-spacing: 0;
  }  

  h1 {
    margin: 0;
    font-size: clamp(2.8rem, 4vw, 4.4rem);
    line-height: 1.02;
    max-width: 14ch;
  }

  .intro-text {
    margin: 24px 0 0;
    color: rgba(27, 31, 26, 0.8);
    font-size: 1rem;
    line-height: 1.8;
    max-width: 42rem;
  }

  .stats-grid {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-top: 32px;
    width: 140px;
  }

  .stat-card {
    background: #ffffff;
    border: 1px solid rgba(111, 155, 99, 0.2);
    border-radius: 12px;
    padding: 12px 14px;
    text-decoration: none;
    color: inherit;
    transition: transform 0.3s ease, box-shadow 0.3s ease, background 0.3s ease, border-color 0.3s ease;
    cursor: pointer;
    text-align: center;
  }

  .stat-card:hover {
    background: #DFE8D9;
    border-color: #6F9B63;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(111, 155, 99, 0.2);
  }

  .stats-grid strong {
    display: block;
    font-size: 1.2rem;
    color: #1b1f1a;
  }

  .stats-grid span {
    color: rgba(27, 31, 26, 0.65);
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 0.06em;
  }

  .country-overview {
    padding: 80px 36px;
  }

  .section-header {
    max-width: 780px;
    margin: 0 auto 42px;
    text-align: center;
  }

  .section-label {
    margin: 0 0 12px;
    color: #6f9b63;
    font-size: 0.82rem;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    font-weight: 700;
  }

  .country-grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 24px;
    max-width: 1200px;
    margin: 0 auto;
  }

  .country-card {
    display: flex;
    flex-direction: column;
    gap: 18px;
    padding: 24px;
    border-radius: 28px;
    background: #ffffff;
    border: 1px solid transparent;
    box-shadow: 0 18px 36px rgba(27, 31, 26, 0.06);
    text-decoration: none;
    color: inherit;
    transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease;
  }

  .country-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 24px 48px rgba(111, 155, 99, 0.16);
    border-color: #6f9b63;
    background: #DFE8D9;
  }

  .country-card-top {
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .country-card-top strong {
    display: block;
    font-size: 1.1rem;
  }

  .country-card-top p {
    margin: 4px 0 0;
    color: rgba(27, 31, 26, 0.65);
    font-size: 0.95rem;
  }

  .country-cities {
    margin: 0;
    color: rgba(27, 31, 26, 0.75);
    line-height: 1.7;
  }

  .country-image {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    object-fit: contain;
  }

  .cities-container {
    max-width: 1180px;
    margin: 0 auto;
    padding: 0 36px;
  }

  .country-block {
    margin-bottom: 64px;
  }

  .country-block h3 {
    margin-bottom: 24px;
    font-size: 1.5rem;
  }

  .city-grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 20px;
    margin-bottom: 24px;
  }

  .city-detail {
    padding: 32px;
    background: #ffffff;
    border-radius: 20px;
    margin-top: 24px;
    border: 1px solid #DFE8D9;
    box-shadow: 0 4px 12px rgba(27, 31, 26, 0.1);
  }

  .city-detail button {
    background: none;
    border: none;
    font-size: 0.9rem;
    cursor: pointer;
    margin-bottom: 16px;
    color: #6F9B63;
    font-weight: 600;
  }

  .city-detail h2 {
    margin: 0 0 8px;
    font-size: 1.6rem;
  }

  .city-detail p {
    margin: 4px 0;
    color: rgba(27, 31, 26, 0.75);
  }

  .city-detail p:last-of-type {
    margin-top: 12px;
    color: rgba(27, 31, 26, 0.8);
  }

  .places-chips {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 16px;
  }

  .place-chip {
    display: inline-block;
    padding: 8px 12px;
    background: #DFE8D9;
    border-radius: 20px;
    text-decoration: none;
    color: #1b1f1a;
    font-size: 0.9rem;
    transition: background 0.3s ease, color 0.3s ease;
  }

  .place-chip:hover {
    background: #6F9B63;
    color: #fff;
  }

  .city-card {
    background: #ffffff;
    border: 1px solid transparent;
    border-radius: 16px;
    padding: 20px;
    text-align: left;
    cursor: pointer;
    transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease;
    box-shadow: 0 4px 12px rgba(27, 31, 26, 0.1);
  }

  .city-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 24px 48px rgba(111, 155, 99, 0.16);
    border-color: #6f9b63;
    background: #DFE8D9;
  }

  .city-card strong {
    display: block;
    margin-bottom: 10px;
    font-size: 1.1rem;
  }

  footer {
    background: #f5f5f0;
    border-top: 1px solid rgba(111, 155, 99, 0.15);
    padding: 48px 36px;
    margin-top: 60px;
  }

  .footer-content {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 48px;
  }

  .footer-main p {
    margin: 0;
    color: rgba(27, 31, 26, 0.7);
    font-size: 0.95rem;
  }

  .footer-credit {
    text-align: right;
  }

  .footer-credit p {
    margin: 4px 0;
    color: rgba(27, 31, 26, 0.6);
    font-size: 0.9rem;
  }

  @media (max-width: 1080px) {
    .hero-inner {
      grid-template-columns: 1fr;
    }

    .country-grid {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }

    .city-grid {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }
  }

  @media (max-width: 760px) {
    .hero {
      padding: 28px 20px;
    }

    .country-grid,
    .city-grid {
      grid-template-columns: 1fr;
    }

    .footer-content {
      flex-direction: column;
      align-items: flex-start;
      gap: 24px;
    }

    .footer-credit {
      text-align: left;
    }
  }

  @media (max-width: 520px) {
    .stats-grid {
      grid-template-columns: 1fr;
    }

    .section-header,
    .country-overview {
      padding: 48px 20px;
    }

    .hero {
      padding-top: 24px;
    }
  }
  
  @media (max-width: 768px) {
  .hero {
    padding: 32px 24px 72px;
  }

  .hero-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 20px;
  }

  nav {
    display: flex;
    gap: 20px;
    font-size: 0.95rem;
  }

  .hero-inner {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 56px;
    margin-top: 72px;
  }

  .hero-left h1 {
    font-size: clamp(3.4rem, 14vw, 5rem);
    line-height: 0.96;
    letter-spacing: -0.05em;
  }

  .intro-text {
    font-size: 1.15rem;
    line-height: 1.7;
    max-width: 100%;
  }

  .hero-right {
    width: 100%;
    justify-self: auto;
  }

  .stats-grid {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr;
    gap: 18px;
    justify-items: center;
  }

  .stat-card {
    width: 140px;
  }

  .city-card,
  .city-card:visited,
  .city-card:hover,
  .city-card:active {
    color: #1b1f1a;
    text-decoration: none;
  }
}
</style>
