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
  if (typeof window !== "undefined") {
    document.querySelector("input#notetitle").focus();
  }
</script>

<link rel="icon" href="/favicons/Rocket.png" />
<title>{noteTitle}</title>
<!-- ✨ Note Editor -->
<br />
<input
  type="text"
  id="notetitle"
  placeholder="Title"
  on:input={refreshNoteTitle}
  on:change={() => document.querySelector("textarea#notecontent").focus()}
/>
<br />
<textarea on:input={OnInput} type="text" id="notecontent" />

<style lang="scss">
  @import url("https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,200..1000;1,200..1000&display=swap");
  :root {
    --md-sys-font-main: Nunito;
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
      opacity: 0.3;
    }
  }
  textarea#notecontent {
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
