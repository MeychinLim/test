<template>
  <div class="relative p-20">
    <county-detail-dialog
      :country="country"
      :visible="isDisplayed"
      :class="isDisplayed ? 'bg-black/50 h-full' : ''"
      class="fixed top-0 left-0 z-30"
    />

    <div class="bg-white p-8 rounded-xl shadow-sm z-20">
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

        <tr v-for="country in countries">
          <td class="p-2 border">
            <img :src="country?.flags?.png" class="rounded-md" />
          </td>
          <td class="p-2 border">
            <div
              @click="showCountryDetail(country?.name?.official)"
              class="hover:cursor-pointer"
            >
              {{ country?.name?.official }}
            </div>
          </td>
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
            <div
              v-if="country?.idd?.suffixes?.length > 0"
              class="flex flex-wrap"
            >
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
  </div>
</template>

<script setup>
const { data: countries } = await useFetch(
  "https://restcountries.com/v3.1/all"
);

const isDisplayed = ref(false);
const country = ref({});

async function showCountryDetail(name) {
  const { data } = await useFetch(
    `https://restcountries.com/v3.1/name/${name}`
  );
  country.value = data.value[0];
  isDisplayed.value = true;
}
</script>
