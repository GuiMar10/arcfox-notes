<script>
  // 🤖 Function to get elements using DOM
  function getElem(element) {
    return document.querySelector(element);
  }

  var noteTitle = "Nota sem título";
  function refreshNoteTitle() {
    if (getElem("input#notetitle").value == "") {
      noteTitle = "Nota sem título";
    } else {
      noteTitle = getElem("input#notetitle").value;
    }
  }

  // 🤞 Function to get CSS variables easily
  function getCSSVariable(variable) {
    return getComputedStyle(document.body).getPropertyValue(variable);
  }
  // 📖 Saves as a ✨ beautiful ✨ vanilla HTML file.
  function saveAsHTML() {
    const noteContent = document.getElementById("notecontent").value;
    const blob = new Blob(
      [
        "<!DOCTYPE html>",
        "<meta charset='UTF-8'>",
        `<title>${noteTitle}</title>`,
        "<link rel='preconnect' href='https://fonts.googleapis.com' />",
        "<link rel='preconnect' href='https://fonts.gstatic.com' crossorigin />",
        "<link href='https://fonts.googleapis.com/css2?family=Inter:wght@200;700;800&display=swap' rel='stylesheet'/>",
        `<style>:root{--md-sys-color-primary: ${getCSSVariable(
          "--md-sys-color-primary-light"
        )}; --md-sys-color-primary-container: ${getCSSVariable(
          "--md-sys-color-primary-container-light"
        )}; --md-sys-color-background: ${getCSSVariable(
          "--md-sys-color-background-light"
        )}; --md-sys-color-on-background: ${getCSSVariable(
          "--md-sys-color-on-background-light"
        )}} @media (prefers-color-scheme: dark){:root{--md-sys-color-primary: ${getCSSVariable(
          "--md-sys-color-primary-dark"
        )}; --md-sys-color-primary-container: ${getCSSVariable(
          "--md-sys-color-primary-container-dark"
        )}; --md-sys-color-background: ${getCSSVariable(
          "--md-sys-color-background-dark"
        )}; --md-sys-color-on-background: ${getCSSVariable(
          "--md-sys-color-on-background-dark"
        )}}}</style>`,
        "<body style='padding: 3.25rem; background: var(--md-sys-color-background)'>",
        `<span style='color: var(--md-sys-color-primary); background: var(--md-sys-color-primary-container); font-family: Inter; display: inline-block;font-weight: 700;font-size: 1.3rem; padding: 6px 14px;
        border-radius: 100px;'>${
          getElem("span#notesubjectlabel").innerHTML
        }</span>`,
        "<h1 style='color: var(--md-sys-color-on-background); font-family: Inter;margin-top: 15px;border: 0;font-size: 3.25rem;font-style: normal;font-weight: 700;'>",
        noteTitle,
        "</h1>",
        "<textarea readonly style='color: var(--md-sys-color-on-background); background: 0; font-family: Inter;font-size: 1.4375rem;font-style: normal;font-weight: 600; margin-top: -20px; width: calc(100% - 3.25rem); height: 90vh; resize: none; border: 0; outline: 0;'>",
        noteContent,
        "</textarea>",
        "</body>",
      ],
      {
        type: "text/html",
      }
    );
    const url = URL.createObjectURL(blob);

    const a = document.createElement("a");
    a.href = url;
    a.download = noteTitle;
    a.click();

    URL.revokeObjectURL(url);
  }
  // 💡 Auto-growing textarea (from DreamTeK - Stack Overflow: https://stackoverflow.com/questions/454202/creating-a-textarea-with-auto-resize)
  if (typeof window !== "undefined") {
    const tx = document.getElementsByTagName("textarea");
    for (let i = 0; i < tx.length; i++) {
      tx[i].setAttribute(
        "style",
        "height:" + tx[i].scrollHeight + "px;overflow-y:hidden;"
      );
    }
  }

  function OnInput() {
    this.style.height = 0;
    this.style.height = this.scrollHeight + "px";
  }
</script>

<link rel="icon" href="/favicons/Rocket.png" />
<title>{noteTitle}</title>
<!-- ✨ Note Editor -->
<span id="notesubjectlabel" contenteditable="true" />
<br />
<input
  type="text"
  id="notetitle"
  placeholder="Title"
  on:input={refreshNoteTitle}
/>
<br />
<textarea on:input={OnInput} type="text" id="notecontent" />

<style lang="scss">
  @import url("https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,200..1000;1,200..1000&display=swap");
  :root {
    --md-sys-font-main: Nunito;
    --md-sys-color-outline: rgb(200, 200, 200);
  }
  @media screen and (max-width: 600px) {
    :global(body) {
      padding: 1.8rem;
    }
  }
  @media screen and (min-width: 600px) {
    :global(body) {
      padding: 3.75rem;
    }
  }
  :global(body) {
    background: var(--md-sys-color-background);
  }
  input#notetitle {
    color: #231866;
    font-family: var(--md-sys-font-main);
    margin-top: 15px;
    border: 0;
    outline: 0;
    width: calc(100% - 1rem);
    height: 20%;
    font-size: 3.25rem;
    font-style: normal;
    font-weight: 800;
    line-height: normal;
    background: none;
    animation: welcomeanimation 0.5s;
    &::placeholder {
      color: var(--whale-text-color);
      opacity: 0.3;
    }
  }
  textarea#notecontent {
    color: var(--whale-text-color);
    background: none;
    font-family: var(--md-sys-font-main);
    font-size: 1.4375rem;
    font-style: normal;
    font-weight: 600;
    margin-top: 10px;
    line-height: normal;
    border: 0;
    outline: 0;
    width: calc(100% - 10px);
    height: 100vh;
    text-align: left;
    resize: none;
    animation: welcomeanimation 0.5s;
    &::placeholder {
      color: var(--whale-text-color);
      opacity: 0.3;
    }
  }
  span#notesubjectlabel {
    font-family: var(--md-sys-font-main);
    display: none;
    font-weight: 700;
    font-size: 1.3rem;
    color: var(--md-sys-color-primary);
    background: var(--md-sys-color-primary-container);
    padding: 6px 14px;
    border-radius: 100px;
    transition: border 2s;
    animation: tagchange 0.5s;
    cursor: pointer;
    &:focus {
      outline: 2px solid var(--md-sys-color-primary);
      cursor: text;
    }
    &:empty {
      background: none;
    }
  }
  @keyframes tagchange {
    from {
      margin-left: -10px;
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
  @keyframes welcomeanimation {
    from {
      margin-left: -10px;
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>
