<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cinnamoroll Tamagotchi</title>
  <style>
    body {
      font-family: 'Comic Sans MS', cursive, sans-serif;
      text-align: center;
      background-color: #fdf0f5;
      color: #333;
    }
    #cinnamoroll {
      width: 200px;
      height: 200px;
      margin: 20px auto;
      background-image: url('placeholder.png'); /* replace with your art */
      background-size: contain;
      background-repeat: no-repeat;
    }
    button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 18px;
      border-radius: 10px;
      border: none;
      background-color: #ffcee3;
      cursor: pointer;
    }
    button:hover {
      background-color: #ffc0cb;
    }
    #stats {
      margin-top: 20px;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <h1>Cinnamoroll Tamagotchi 🐾</h1>
  <div id="cinnamoroll"></div>

  <div>
    <button onclick="feed()">Feed 🥐</button>
    <button onclick="play()">Play 🎾</button>
    <button onclick="sleep()">Sleep 💤</button>
    <button onclick="randomEvent()">Surprise Event ✨</button>
  </div>

  <div id="stats"></div>

  <script>
    class CinnaTama {
      constructor(name) {
        this.name = name;
        this.age = 0;
        this.hunger = 50;
        this.happiness = 50;
        this.energy = 50;
        this.stage = "Puppy";
      }

      feed(amount = 10) {
        this.hunger += amount;
        if(this.hunger > 100) this.hunger = 100;
        this.happiness += 5;
        this._checkGrowth();
        updateStats();
      }

      play(amount = 10) {
        this.happiness += amount;
        this.energy -= 10;
        if(this.happiness > 100) this.happiness = 100;
        if(this.energy < 0) this.energy = 0;
        this._checkGrowth();
        updateStats();
      }

      sleep(amount = 20) {
        this.energy += amount;
        this.hunger -= 5;
        if(this.energy > 100) this.energy = 100;
        if(this.hunger < 0) this.hunger = 0;
        updateStats();
      }

      passTime(days = 1) {
        this.age += days;
        this.hunger -= 10 * days;
        this.happiness -= 5 * days;
        this.energy -= 10 * days;
        if(this.hunger < 0) this.hunger = 0;
        if(this.happiness < 0) this.happiness = 0;
        if(this.energy < 0) this.energy = 0;
        this._checkGrowth();
        updateStats();
      }

      _checkGrowth() {
        if(this.age < 3) this.stage = "Puppy";
        else if(this.age < 7) this.stage = "Chubby Cinnamoroll";
        else this.stage = "Fluffy Adult";
      }

      randomEvent() {
        const events = [
          `${this.name} chased a yarn ball!`,
          `${this.name} spilled some milk!`,
          `${this.name} napped peacefully!`,
          `${this.name} got a visit from Croissant!`,
          `${this.name} did a happy twirl!`
        ];
        alert(events[Math.floor(Math.random() * events.length)]);
      }

      status() {
        return {
          name: this.name,
          age: this.age,
          hunger: this.hunger,
          happiness: this.happiness,
          energy: this.energy,
          stage: this.stage
        };
      }
    }

    // Initialize your Cinnamoroll
    const myCinna = new CinnaTama("Cinna");

    function updateStats() {
      const s = myCinna.status();
      document.getElementById('stats').innerHTML = `
        Name: ${s.name} <br>
        Stage: ${s.stage} <br>
        Age: ${s.age} day(s) <br>
        Hunger: ${s.hunger} <br>
        Happiness: ${s.happiness} <br>
        Energy: ${s.energy}
      `;
    }

    function feed() { myCinna.feed(); }
    function play() { myCinna.play(); }
    function sleep() { myCinna.sleep(); }
    function randomEvent() { myCinna.randomEvent(); }

    updateStats();
  </script>
</body>
</html>
