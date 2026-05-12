
document.addEventListener('DOMContentLoaded', function() {
  $("#navbar").load("header.html");
  $("#footer").load("footer.html");

  if (document.title === "Contact"){
    document.getElementById("contactForm").addEventListener('submit', function(event) {
      contactFormSubmit(event)
    });
  }

})

function nav_loaded(){
  console.log("nav-loaded")
  const listItems = document.querySelectorAll('.nav-link');
  for (item of listItems){
    if (item.id != document.title){
      item.classList.remove('active')
    }
    else{
      item.classList.add('active')
    }
  }

    /**
  * Utility function to calculate the current theme setting.
  * Look for a local storage value.
  * Fall back to system setting.
  * Fall back to light mode.
  */
  function calculateSettingAsThemeString({ localStorageTheme, systemSettingDark }) {
    if (localStorageTheme !== null) {
      return localStorageTheme;
    }

    if (systemSettingDark.matches) {
      return "dark";
    }

    return "light";
  }


  /**
  * Utility function to update the button text and aria-label.
  */
  function updateButton({ buttonEl, isDark }) {
    const newCta = isDark ? "Change to light theme" : "Change to dark theme";
    const newImg = isDark ? "assets/dark_mode.svg" : "assets/light_mode.svg";
    buttonEl.setAttribute("aria-label", newCta);
    buttonImage.setAttribute("src", newImg)
  }

  /**
  * Utility function to update the theme setting on the html tag
  */
  function updateThemeOnHtmlEl({ theme }) {
    document.querySelector("html").setAttribute("data-bs-theme", theme);
  }


/**
 * Utility function to update logos to dark mode
 */
  function updateImg({isDark}){
    const imgModeChange = document.getElementsByClassName("img-mode-chng")
    for (element of imgModeChange){
      var currentSrc = element.src
      var newSrc = currentSrc.replace( isDark ? "light" : "dark", isDark ? "dark" : "light")
      element.src = newSrc
    }
  }

  /**
  * On page load:
  */

  /**
  * 1. Grab what we need from the DOM and system settings on page load
  */
  const button = document.getElementById("theme-toggle");
  const buttonImage = document.getElementById("theme-toggle-svg")
  const localStorageTheme = localStorage.getItem("theme");
  const systemSettingDark = window.matchMedia("(prefers-color-scheme: dark)");

  /**
  * 2. Work out the current site settings
  */
  let currentThemeSetting = calculateSettingAsThemeString({ localStorageTheme, systemSettingDark });

  /**
  * 3. Update the theme setting and button text accoridng to current settings
  */
  updateButton({ buttonEl: button, isDark: currentThemeSetting === "dark" });
  updateThemeOnHtmlEl({ theme: currentThemeSetting });
  updateImg({isDark: currentThemeSetting === "dark" });

  /**
  * 4. Add an event listener to toggle the theme
  */
  button.addEventListener("click", (event) => {
    const newTheme = currentThemeSetting === "dark" ? "light" : "dark";
    localStorage.setItem("theme", newTheme);
    updateButton({ buttonEl: button, isDark: newTheme === "dark" });
    updateThemeOnHtmlEl({ theme: newTheme });
    updateImg({isDark: newTheme === "dark" })

    currentThemeSetting = newTheme;
  });
}

function loaded(){
  console.log("Loaded test")
}



function contactFormSubmit(event){
  event.preventDefault()
  var subject = document.getElementById("emailFormSubject").value
  var body = document.getElementById("emailFormBody").value
  var mailto = `mailto:swindlehurstw20@josephwhitaker.org?subject=Website%20Contact%20Form: ${subject}&body=${body}`
  window.location.href = mailto
}

