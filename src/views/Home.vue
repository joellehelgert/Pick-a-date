<template>
  <div class="home">
    <h1 class="text-red-500">VRS Masterarbeitsstudie Joelle</h1>
    <p>Vielen Dank erstmal, dass du an meiner User Study teilnimmst!🥳</p>
    <p>
      Im Rahmen der Studie musst du mit meiner selbst gebauten Messstudie 3
      verschiedene Anwendungen testen und davor und danach einen Fragebogen
      ausfüllen. Das dauert ca. 30 Minuten pro Anwendung. Das einzige "Problem"
      ist, dass du zwischen den Anwendungen eine Pause von mindestens 60 Minuten
      machen musst. Deshalb würde ich dich bitten, dir im nächsten Schritt 3
      Termine auszusuchen, an denne du Zeit und Lust hast das ganze zu machen.
      Die User Study selbst findet am FH Campus Hagenberg (FH 2 Ebene 3 Raum
      ---) statt. Je nach Anreise etc kannst du gern in den Wartezeiten bei uns
      zu Hause im Garten etwas entspannen. Für Snacks und Getränke ist auf jeden
      Fall gesorgt!
    </p>

    <router-link
      class="
        p-3
        bg-yellow-100 bg-greenSheen
        border border-greenSheen
        text-white
      "
      to="/selection"
      >Zur Terminauswahl</router-link
    >
    <router-link
      class="
        p-3
        ml-3
        bg-yellow-100 bg-greenSheen
        border border-greenSheen
        text-white
      "
      to="/overview"
      >Zur Terminübersicht
    </router-link>
  </div>
</template>

<script>
export default {
  name: "Home",
  components: {},
};
</script>
