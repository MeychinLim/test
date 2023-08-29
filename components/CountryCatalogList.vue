<template>
  <div class="bg-white p-8 rounded-xl shadow-sm">
    <table class="text-sm">
      <tr class="bg-gray-100">
        <th class="p-2 border" rowspan="2">Flags</th>
        <th class="p-2 border" rowspan="2">Country Name</th>
        <th class="p-2 border" colspan="2">Country Code</th>
        <th class="p-2 border" rowspan="2">Native Country Name</th>
        <th class="p-2 border" rowspan="2">Alternative Country Name</th>
        <th class="p-2 border" rowspan="2">Country Calling Codes</th>
      </tr>
      <tr class="bg-gray-100">
        <th class="p-2 border w-32">2 Character</th>
        <th class="p-2 border w-32">3 Character</th>
      </tr>
      <tr v-for="(country, index) in countries">
        <td class="p-2 border"><img :src="country?.flags?.png" /></td>
        <td class="p-2 border">{{ country?.name?.official }}</td>
        <td class="p-2 border">{{ country?.cca2 }}</td>
        <td class="p-2 border">{{ country?.cca3 }}</td>
        <td class="p-2 border">
          <span v-if="country?.name?.nativeName">
            {{ Object.values(country.name.nativeName)[0].official }}
          </span>
          <span v-else> N/A </span>
        </td>
        <td class="p-2 border">
          <span v-for="(altSpelling, index) in country?.altSpellings">
            {{ altSpelling }}
            <span v-if="country?.altSpellings?.length > index + 1"> , </span>
          </span>
        </td>
        <td class="p-2 border w-96">
          <div v-if="country?.idd?.suffixes?.length > 0" class="flex flex-wrap">
            <span v-for="(suffix, index) in country?.idd?.suffixes">
              {{ country?.idd?.root + suffix }}
              <span
                v-if="country?.idd?.suffixes?.length > index + 1"
                class="mr-1"
              >
                ,
              </span>
            </span>
          </div>
          <span v-else> N/A </span>
        </td>
      </tr>
    </table>
  </div>
</template>

<script setup>
const { data: countries } = await useFetch(
  "https://restcountries.com/v3.1/all"
);
</script>
