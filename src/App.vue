<template>
  <div id="header">
    <div class="container">
      <nav>
        <img src="./assets/img/noel2.png" class="logo" />
        <ul id="sidemenu">
          <li><a href="#header">Home</a></li>
          <li><a href="#about">About</a></li>
          <li><a href="#MyApp">Portfolio</a></li>
          <li><a href="#contact">Contact</a></li>
          <i class="fas fa-times" @click="closemenu"></i>
        </ul>
        <i class="fas fa-bars" @click="openmenu"></i>
      </nav>

      <!--header-->

      <div class="header-text">
        <div class="rounded-image-container">
          <img
            class="rounded-image"
            src="/src/assets/img/Noel.jpg"
            alt="Your Alt Text"
          />
        </div>
        <p>Web Development</p>
        <h1>
          Hi, I'm <span>Noel</span><br />
          As Daniel Padilla
        </h1>

        <div class="social-icons">
          <a href="#"><i class="fab fa-twitter-square"></i></a>
          <a href="#"><i class="fab fa-facebook"></i></a>
          <a href="#"><i class="fab fa-linkedin"></i></a>
          <a href="#"><i class="fab fa-instagram"></i></a>
        </div>
      </div>
    </div>
  </div>
  <!--About-->
  <div id="about">
    <div class="container">
      <div class="row">
        <div class="about-col-1">
          <img src="../src/assets/img/Noel.jpg" />
        </div>
        <div class="about-col-2">
          <h1 class="sub-title">About <span>Me</span></h1>
          <h3 style="color: blue">Hello, I'm Noel Daguipa! <br /><br /></h3>
          <p style="color: black">
            <!-- Your about me content goes here -->
            "I'm a passionate web developer and back-end developer with a love
            for crafting innovative and efficient digital solutions. Hailing
            from the vibrant City of Lapu-Lapu, I draw inspiration from the
            dynamic surroundings and cultural richness that characterize my
            hometown. My journey in the world of coding began with a curiosity
            to understand the intricate workings of the web. Today, I thrive on
            turning ideas into functional, user-friendly applications that make
            a meaningful impact. As I continue to explore the ever-evolving
            landscape of web development, I am excited to contribute my skills
            and create seamless online experiences for users around the globe."
          </p>

          <div class="tab-title">
            <p class="tab-links active-link" @click="opentab('education')">
              Education
            </p>
            <p class="tab-links" @click="opentab('skills', $event)">Skills</p>
            <p class="tab-links" @click="opentab('experience', $event)">
              TodoApp
            </p>
          </div>

          <div class="tab-contents active-tab" id="education">
            <ul>
              <li><span>2021-2023</span><br />BSIT CORDOVA PUBLIC COLLEGE</li>
            </ul>
          </div>
          <div class="tab-contents" id="skills">
            <ul>
              <li><span>Web Developer</span><br />Web Development</li>
              <li><span>UI/UX</span><br />Web Designing</li>
            </ul>
          </div>
          <div class="tab-contents" id="experience"></div>
        </div>
      </div>
    </div>
  </div>

  <div class="services">
    <div class="container">
      <h1 class="sub-title">My <span>ToDo App</span></h1>
    </div>
  </div>
  <div>
    <div id="app" class="todo">
      <h1>ToDo App</h1>

      <input
        v-model="newTask"
        @keyup.enter="addTask"
        placeholder="Add a new task"
      />

      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          {{ task }}
          <button @click="editTask(index)">Edit</button>
          <button @click="deleteTask(index)">Delete</button>
        </li>
      </ul>

      <button @click="clearAll">Clear All</button>

      <input v-model="search" placeholder="Search tasks" @input="filterTasks" />

      <ul>
        <li v-for="(task, index) in filteredTasks" :key="index">
          {{ task }}
        </li>
      </ul>
    </div>
  </div>

  <!-- Portfolio Design -->
  <div id="app">
    <div id="portfolio">
      <div class="container">
        <h1 class="sub-title">Unique <span>Application</span></h1>

        <div class="speech-app">
          <input v-model="sentence" placeholder="Enter a sentence" />
          <button @click="speak">Speak</button>
        </div>
      </div>
    </div>
  </div>
  <!-- Contact section -->
  <div class="contact">
    <div class="container">
      <div class="row">
        <div class="contact-left">
          <h1 class="sub-title">Contact<span> Us</span></h1>
          <p><i class="fa-solid fa-share"></i>noeldaguipa@gmail.com</p>
          <p><i class="fa-solid fa-phone"></i>092012354382</p>

          <div class="social-icons">
            <a href="#"><i class="fab fa-facebook"></i></a>
            <a href="https://instagram.com/"
              ><i class="fab fa-instagram"></i
            ></a>
            <a href="#"><i class="fab fa-twitter-square"></i></a>
            <a href="#"><i class="fab fa-linkedin"></i></a>
          </div>
          <a href="../src/assets/img/android.jpeg" download class="btn btn2"
            >Download CV</a
          >
        </div>
        <div class="contact-right">
          <form>
            <input type="text" name="Name" placeholder="Your Name" required />
            <input
              type="email"
              name="email"
              placeholder="Your Email"
              required
            />
            <textarea
              name="Message"
              rows="6"
              placeholder="Your Message"
            ></textarea>
            <button type="submit" class="btn btn2">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
      editingIndex: null,
      search: "",
      tablinks: [],
      tabcontents: [],
      sidemenu: null,
      sentence: "",
    };
  },
  mounted() {
    this.tablinks = document.getElementsByClassName("tab-links");
    this.tabcontents = document.getElementsByClassName("tab-contents");
    this.sidemenu = document.getElementById("sidemenu");

    // Check if sidemenu is null before proceeding
    if (this.sidemenu) {
      this.sidemenu.addEventListener("click", this.closemenu);
    }
  },
  computed: {
    filteredTasks() {
      return this.tasks.filter((task) => task.includes(this.search));
    },
  },
  methods: {
    opentab(tabname, event) {
      for (const tablink of this.tablinks) {
        tablink.classList.remove("active-link");
      }
      for (const tabcontent of this.tabcontents) {
        tabcontent.classList.remove("active-tab");
      }

      if (event && event.currentTarget) {
        event.currentTarget.classList.add("active-link");
      }

      const tabElement = document.getElementById(tabname);
      if (tabElement) {
        tabElement.classList.add("active-tab");
      }
    },
    openmenu() {
      if (this.sidemenu) {
        this.sidemenu.style.right = "0";
      }
    },
    closemenu() {
      if (this.sidemenu) {
        this.sidemenu.style.right = "-200px";
      }
    },
    addTask() {
      if (this.newTask.trim() !== "") {
        if (this.editingIndex !== null) {
          this.$set(this.tasks, this.editingIndex, this.newTask);
          this.editingIndex = null;
        } else {
          this.tasks.push(this.newTask);
        }
        this.newTask = "";
      }
    },
    editTask(index) {
      this.newTask = this.tasks[index];
      this.editingIndex = index;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    clearAll() {
      this.tasks = [];
    },
    speak() {
      if (this.sentence.trim() !== "") {
        const speechSynthesis = window.speechSynthesis;
        const utterance = new SpeechSynthesisUtterance(this.sentence);

        speechSynthesis.speak(utterance);
      }
    },
  },
};
</script>
