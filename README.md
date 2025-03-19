<!DOCTYPE html>
<html>
<head>
    <title>Portfolio - Evangeline Joshna</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background: #84a6e9;
        }

        header {
            background-color: #941919;
            color: #fff;
            text-align: center;
            padding: 2rem 0;
            position: relative;
        }

        .profile-picture {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            object-fit: cover;
            position: absolute;
            top: 75px;
            left: 75px;
        }

        nav {
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 10px 0;
        }

        nav ul {
            list-style-type: none;
        }

        nav ul li {
            display: inline;
            margin: 0 20px;
        }

        nav ul li a {
            text-decoration: none;
            color: #fff;
            font-size: 1.2rem;
        }

        .section-content {
            background-color: #fff;
            padding: 2rem;
            margin: 1rem;
            border-radius: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: justify;
        }

        .download-button {
            background-color: #333;
            color: #fff;
            padding: 0.5rem 1rem;
            text-decoration: none;
            border-radius: 20px;
            display: inline-block;
            margin-top: 10px;
        }

        .download-button:hover {
            background-color: #555;
        }

        footer {
            text-align: center;
            padding: 1rem 0;
            background-color: #333;
            color: #fff;
        }

        #tasks {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin: 1rem;
        }

        #list-container {
            margin-top: 10px;
        }

        #item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            background: #fff;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin-bottom: 10px;
        }

        #delete {
            background-color: #e63946;
            color: #fff;
            padding: 5px 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #delete:hover {
            background-color: #f72536;
            transform: scale(1.1);
            transition: 0.2s;
        }
    </style>
</head>
<body>
    <header>
        <div class="header-content">
            <img src="https://media.licdn.com/dms/image/v2/D5603AQFzTaeQt9k-jA/profile-displayphoto-shrink_200_200/B56ZWsQcy6HEAY-/0/1742351752057?e=2147483647&v=beta&t=TzZjZlZPxOdPJYqgPKQPvMppSVYadSIoffKYaepcrHs" alt="Evangeline Joshna" class="profile-picture">
            <h1>Evangeline Joshna</h1>
            <p>II B.Sc IT | Aspiring Web Developer</p>
        </div>
    </header>

    <nav>
        <ul>
            <li><a href="#about">About</a></li>
            <li><a href="#education">Education</a></li>
            <li><a href="#skills">Skills</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#resume">Resume</a></li>
            <li><a href="#tasks">To-Do List</a></li>
        </ul>
    </nav>

    <section id="about" class="section-content">
        <h2>About Me</h2>
        <p>I'm a passionate web developer currently pursuing B.Sc IT at Sri Ramakrishna College of Arts and Science for Women.</p>
    </section>

    <section id="education" class="section-content">
        <h2>Education</h2>
        <p>II B.Sc Information Technology | Sri Ramakrishna College of Arts and Science for Women</p>
    </section>

    <section id="skills" class="section-content">
        <h2>Skills</h2>
        <ul>
            <li>HTML, CSS, JavaScript</li>
            <li>React.js, Node.js, Express.js</li>
            <li>MongoDB, SQL</li>
            <li>Python, Java</li>
            <li>Cloud Computing, AI & ML</li>
        </ul>
    </section>

    <section id="projects" class="section-content">
        <h2>Projects</h2>
        <ul>
            <li><a href="#">E-Commerce Website</a></li>
            <li><a href="#">Cloud Security Implementation</a></li>
            <li><a href="#">AI Chatbot using IBM Watson</a></li>
            <li><a href="#">College Portal Development</a></li>
        </ul>
    </section>

    <section id="resume" class="section-content">
        <h2>Resume</h2>
        <a href="Curriculam_vitae-EVANGELINE.pdf" target="_blank" class="download-button">Download CV</a>
    </section>

    <section id="tasks" class="section-content">
        <h2>To-Do List</h2>
        <form id="task-form">
            <input type="text" id="input" placeholder="Enter a task">
            <button type="submit">Add</button>
        </form>
        <ul id="list-container"></ul>
    </section>

    <footer>
        <p>&copy; 2025 Evangeline Joshna</p>
    </footer>

    <script>
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                const targetId = this.getAttribute('href').substring(1);
                const targetElement = document.getElementById(targetId);
                if (targetElement) {
                    window.scrollTo({
                        top: targetElement.offsetTop,
                        behavior: 'smooth'
                    });
                }
            });
        });

        const inputEl = document.querySelector("#input");
        const outputEl = document.querySelector("#list-container");
        const form = document.querySelector("#task-form");

        function getTasks() {
            let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
            outputEl.innerHTML = tasks.map(task => 
                `<li id="item">
                    <span>${task.title}</span>
                    <button onclick="removeTask('${task.id}')" id="delete">X</button>
                </li>`).join("");
        }

        function addTask(e) {
            e.preventDefault();
            if (!inputEl.value.trim()) return alert("Please enter a task");

            let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
            tasks.unshift({ id: Date.now(), title: inputEl.value.trim() });
            localStorage.setItem("tasks", JSON.stringify(tasks));
            inputEl.value = "";
            getTasks();
        }

        function removeTask(id) {
            let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
            tasks = tasks.filter(task => task.id !== +id);
            localStorage.setItem("tasks", JSON.stringify(tasks));
            getTasks();
        }

        form.addEventListener("submit", addTask);
        getTasks();
    </script>
</body>
</html>
