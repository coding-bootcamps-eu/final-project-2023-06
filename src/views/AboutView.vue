<template>
  <div class="about">
    <h1>About us</h1>

    <details>
      <summary>Students</summary>
      <ul>
        <li v-for="member in students" :key="member.name">
          {{ member.name }} 
          <a :href="member.githubProfile" target="_blank">GitHub</a>
        </li>
      </ul>
    </details>

    <details >
      <summary>Staff</summary>
      <ul>
        <li v-for="member in staff" :key="member.name">
          {{ member.name }} 
          <a :href="member.githubProfile" target="_blank">GitHub</a>
        </li>
      </ul>
    </details>

    <details >
      <summary>School</summary>
      <ul>
        <li >
          
          <a href="https://www.coding-bootcamps.eu/" target="_blank">CBE</a>
        </li>
      </ul>
    </details>
  </div>
</template>

<script>
export default {
  data() {
    return {
      students: [
        { name: 'Berkant Cetin', githubProfile: 'https://github.com/Beggsn' },
        { name: 'Marcelo Lützenkirchen', githubProfile: 'https://github.com/MeloLytz' },
        // Weitere Schüler hier hinzufügen
      ],
      staff: [
        { name: 'Gabriel Heinrich', githubProfile: 'https://github.com/gabrielheinrich' },
        { name: 'Joe Ray Gregory', githubProfile: 'https://github.com/joegregory-cbe' },
        { name: 'Ferdinand Niemann', githubProfile: 'https://github.com/ferniemann' },
        { name: 'Nina Märte', githubProfile: 'https://github.com/NonoSikk' },
        // Weitere Lehrer hier hinzufügen
      ],
    };
  },
};
</script>