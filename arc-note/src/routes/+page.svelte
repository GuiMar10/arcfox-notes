<script>
  // 🤖 Function to get elements using DOM
  function getElem(element) {
    return document.querySelector(element);
  }

  var noteTitle = "Untitled Note";
  function refreshNoteTitle() {
    if (getElem("input#notetitle").value == "") {
      noteTitle = "Untitled Note";
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

  function parseURLParams() {
    var url = "https://split.me/?page1=&page2=";
    if (typeof window !== "undefined") {
      url = window.location.href;
    }
    if (url.includes("?")) {
      var queryStart = url.indexOf("?") + 1,
        queryEnd = url.indexOf("#") + 1 || url.length + 1,
        query = url.slice(queryStart, queryEnd - 1),
        pairs = query.replace(/\+/g, " ").split("&"),
        parms = {},
        i,
        n,
        v,
        nv;

      if (query === url || query === "") return;

      for (i = 0; i < pairs.length; i++) {
        nv = pairs[i].split("=", 2);
        n = decodeURIComponent(nv[0]);
        v = decodeURIComponent(nv[1]);

        if (!parms.hasOwnProperty(n)) parms[n] = [];
        parms[n].push(nv.length === 2 ? v : null);
      }
      return parms;
    } else {
      return {
        notetitle: [""],
        notecontent: [""],
      };
    }
  }
  var notecontentfromurl = "";
  var notetitlefromurl = "";

  if (typeof parseURLParams().notetitle !== "undefined") {
    notetitlefromurl = parseURLParams().notetitle;
  }

  if (typeof parseURLParams().notecontent !== "undefined") {
    notecontentfromurl = parseURLParams().notecontent;
  }

  function OnInput() {
    this.style.height = 0;
    this.style.height = this.scrollHeight + "px";
  }
  if (typeof window !== "undefined") {
    if (notetitlefromurl == "") {
      document.querySelector("input#notetitle").focus();
    }
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
  value={notetitlefromurl}
  on:input={refreshNoteTitle}
  on:change={() => document.querySelector("textarea#notecontent").focus()}
/>
<br />
<textarea
  on:input={OnInput}
  value={notecontentfromurl}
  type="text"
  id="notecontent"
/>

<!--
<input
  on:click={() => document.querySelector("input.copysharelink").select()}
  id="copysharelink"
  readonly
/> 
<button id="sharenotebutton">ios_share</button>
-->

<style lang="scss">
  @import url("https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,200..1000;1,200..1000&display=swap");
  @import url("https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0");
  :root {
    --md-sys-font-main: Nunito;
    --md-sys-on-background: #231866;
    background: #f5f3ff;
  }
  @media screen and (max-width: 600px) {
    :global(body) {
      padding: 1.8rem;
    }
  }
  @media screen and (min-width: 600px) {
    :global(body) {
      padding: 3.75rem;
      text-align: center;
    }
  }
  button#sharenotebutton {
    font-family: Material Symbols Outlined;
    position: fixed;
    bottom: 15px;
    right: 15px;
    width: 50px;
    height: 50px;
    font-size: 24px;
    border: 0;
    cursor: pointer;
    background: transparent;
    color: var(--md-sys-on-background);
  }
  input#copysharelink {
    position: fixed;
    bottom: 70px;
    right: 15px;
  }
  input#notetitle {
    color: var(--md-sys-on-background);
    font-family: var(--md-sys-font-main);
    margin-top: 15px;
    border: 0;
    outline: 0;
    width: calc(60% - 1rem);
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
    width: calc(60% - 1rem);
    height: calc(100vh - 270px);
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
