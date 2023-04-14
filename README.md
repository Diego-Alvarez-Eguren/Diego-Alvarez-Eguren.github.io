<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    
  </head>
  <body>
    <h1>Torre.bio API</h1>
    <form id="bio-form">
      <label for="username-input">Enter a Torre username:</label>
      <input type="text" id="username-input" name="username" />
      <button type="submit">Get user's bio</button>
    </form>
    <div id="bio-container"></div>
    <script>
      const form = document.getElementById("bio-form");
      const usernameInput = document.getElementById("username-input");
      const bioContainer = document.getElementById("bio-container");

      form.addEventListener("submit", event => {
        event.preventDefault();

        const username = usernameInput.value;
        const apiUrl = `https://diego-alvarez-eguren.github.io/https://torre.bio/api/bios/`+username;

        fetch(apiUrl)
          .then(response => response.json())
          .then(data => {
            // Create HTML elements to display the user's bio
            const bioHtml = `
              <h2>${data.person.name}</h2>
              <p>${data.person.professionalHeadline}</p>
              <p>${data.person.location.name}</p>
            `;
            bioContainer.innerHTML = bioHtml;
          })
          .catch(error => {
            console.error(error);
            bioContainer.innerHTML = "<p>There was an error retrieving the user's bio.</p>";
          });
      });
    </script>
  </body>
</html>
