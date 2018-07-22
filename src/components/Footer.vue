<template>
  <footer class="page-footer">
    <div class="container">
      <div class="row">
        <div class="col l6 s12">
          <p class="grey-text text-lighten-4">
            This mini project was created in a day during the week
            of July 16 - July 22 2018. The project effort arises from a concept
            I've written about called
            <span class="blue-text text-lighten-4">Code Something Weekly</span>.
          </p>
          <p>
             <a
              :href="ARTICLE_LINK"
              class="blue-text text-lighten-3">
              Read about C.S Weekly on
              <span class="Medium">M</span>edium.
            </a>
          </p>
        </div>
        <div class="col l4 offset-l2 s12">
          <h5 class="white-text">My Stuff</h5>
          <ul class="header-links">
            <li>
              <a
                :href="GITHUB_LINK"
                class="grey-text text-lighten-3">
                <span class="GIT">G</span>ithub
              </a>
            </li>
            <li>
              <a
                :href="MEDIUM_LINK"
                class="grey-text text-lighten-3">
                <span class="Medium">M</span>edium
              </a>
            </li>
            <li>
              <a
                :href="MIXCLOUD_LINK"
                class="grey-text text-lighten-3">
                <span class="Mixcloud">M</span>ixcloud
              </a>
            </li>
            <li>
              <a
               :href="SO_LINK"
               class="grow grey-text text-lighten-3">
                <span class="SO">S</span>tack Overflow
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="footer-copyright">
      <div class="container">
        © 2018
        <a :href="GITHUB_LINK">
          <span class="copyright">vapurrmaid</span>
        </a>
      </div>
    </div>
  </footer>
</template>

<script>
const ARTICLE_LINK = `https://medium.com/@vapurrmaid/code-something-weekly-how-and-why-44640d279ca1`
const GITHUB_LINK = `https://github.com/vapurrmaid`
const MEDIUM_LINK = `https://medium.com/@vapurrmaid`
const MIXCLOUD_LINK = `https://mixcloud.com/vapurrmaid/uploads`
const SO_LINK = `https://stackoverflow.com/users/8954866/vapurrmaid?tab=profile`

export default {
  name: 'Footer',
  data () {
    return {
      ARTICLE_LINK,
      GITHUB_LINK,
      MEDIUM_LINK,
      MIXCLOUD_LINK,
      SO_LINK
    }
  }
}
</script>

<style>
a:hover {
  cursor: pointer;
}

/* list of links */
.header-links > li {
  margin-bottom: .5em;
}

.header-links > li > a {
  transition: font-size .5s;
}

.header-links > li > a:hover {
  font-size: 1.5em;
}

/* special block letters*/
span.copyright {
  color: #000;
  font-family: 'VT323', monospace;
  letter-spacing: 2px;
}

span.copyright:hover {
  text-decoration: underline;
}

span.GIT {
  background-color: #000;
  border-radius: 10px;
  color: #FFF;
  padding: 0px 5px;
}

span.Medium {
  background-color: #000;
  border: 1px solid #000;
  color: #FFF;
  padding:0 3px;
}

span.Mixcloud {
  background-color: rgba(39,58,75,.97);
  border: 1px solid rgba(39,58,75,.97);
  border-radius: 4px;
  padding: 0 3px;
}

span.SO {
  background: repeating-linear-gradient(
    0deg,
    #ffab05,
    #ffab05 2px,
    #eee 2px,
    #eee 4px
  );
  border: 1px solid #eee;
  border-radius: 4px;
  color: #000;
  padding: 0 5px;
}
</style>
