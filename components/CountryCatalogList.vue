<template>
  <div class="relative p-8">
    <!-- Country details dialog -->
    <county-detail-dialog
      :country="country"
      :visible="isDisplayed"
      :class="isDisplayed ? 'bg-black/50 h-full' : ''"
      class="fixed top-0 left-0 z-30"
    />

    <!-- Search and sort -->
    <div class="flex justify-between mb-4 w-full">
      <input
        v-model="searchName"
        type="input"
        class="bg-white border py-2 px-4 rounded-lg"
        placeholder="Search Country Name"
      />
      <div>
        <label class="mr-2">Sort By</label>
        <select v-model="sortBy" class="bg-white border py-2 px-4 rounded-lg">
          <option value="asc">ASC</option>
          <option value="desc">DESC</option>
        </select>
      </div>
    </div>

    <!-- Countries table -->
    <div class="bg-white p-8 rounded-xl shadow-sm z-20">
      <div class="text-sm pb-2">
        {{ "Result " + paginationData.data.length + " of " + totalCount }}
      </div>
      <table id="pager" class="text-sm">
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

        <tr v-for="country in paginationData.data">
          <td class="p-2 border w-40">
            <img :src="country?.flags?.png" class="rounded-md" />
          </td>
          <td class="p-2 border w-80">
            <div
              @click="showCountryDetail(country?.name?.official)"
              class="hover:cursor-pointer text-blue-400"
            >
              {{ country?.name?.official }}
            </div>
          </td>
          <td class="p-2 border">{{ country?.cca2 }}</td>
          <td class="p-2 border">{{ country?.cca3 }}</td>
          <td class="p-2 border w-80">
            <span v-if="country?.name?.nativeName">
              {{ Object.values(country.name.nativeName)[0].official }}
            </span>
            <span v-else> N/A </span>
          </td>
          <td class="p-2 border w-96">
            <span v-for="(altSpelling, index) in country?.altSpellings">
              {{ altSpelling }}
              <span v-if="country?.altSpellings?.length > index + 1"> , </span>
            </span>
          </td>
          <td class="p-2 border w-52">
            <div
              v-if="country?.idd?.suffixes?.length > 0"
              class="flex flex-wrap"
            >
              <div v-for="(suffix, index) in country?.idd?.suffixes">
                <div v-if="index < 3">
                  <span>{{ country?.idd?.root + suffix }}</span>
                  <span
                    v-if="country?.idd?.suffixes?.length > index + 1"
                    class="mr-1"
                  >
                    ,
                  </span>
                </div>
              </div>
              <span v-if="country?.idd?.suffixes?.length > 3">...</span>
            </div>
            <span v-else> N/A </span>
          </td>
        </tr>
      </table>

      <!-- Pagination -->
      <div class="pt-8">
        <ul class="pagination">
          <li
            class=""
            :class="{ disabled: currentPage === 1 }"
            @click="backToFirstPage()"
          >
            {{ "<<" }}
          </li>
          <li
            class=""
            :class="{ disabled: currentPage === 1 }"
            @click="goToPreviousPage()"
          >
            {{ "<" }}
          </li>
          <li
            v-for="page in paginationData.pages"
            :key="page"
            :class="[
              { active: currentPage === page },
              { hidden: page > currentPage + 2 || page < currentPage - 2 },
            ]"
            @click="handlePageChange(page)"
          >
            {{ page }}
          </li>
          <li
            class=""
            :class="{ disabled: currentPage === paginationData.totalPages }"
            @click="goToNextPage()"
          >
            {{ ">" }}
          </li>
          <li
            class=""
            :class="{ disabled: currentPage === paginationData.totalPages }"
            @click="goToLastPage()"
          >
            {{ ">>" }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
const { data: restCountries } = await useFetch(
  "https://restcountries.com/v3.1/all"
);

const country = ref({});
const isDisplayed = ref(false);
const currentPage = ref(1);
const searchName = ref("");
const sortBy = ref("asc");

const countries = computed(() => {
  if (searchName.value) {
    currentPage.value = 1;

    return restCountries.value
      .filter((country) =>
        country.name.official
          .toLowerCase()
          .includes(searchName.value.toLowerCase())
      )
      .sort((a, b) => {
        if (sortBy.value === "asc") {
          return a.name.official.localeCompare(b.name.official);
        }

        return b.name.official.localeCompare(a.name.official);
      });
  }

  return restCountries.value.sort((a, b) => {
    if (sortBy.value === "asc") {
      return a.name.official.localeCompare(b.name.official);
    }

    return b.name.official.localeCompare(a.name.official);
  });
});

const totalCount = computed(() => countries.value.length);
const paginationData = computed(() => pagination());

const pagination = () => {
  const rowPerPage = 25;
  const start = (currentPage.value - 1) * rowPerPage;
  const end = start + rowPerPage;

  const pages = [];
  for (let i = 1; i <= Math.ceil(totalCount.value / rowPerPage); i++) {
    pages.push(i);
  }

  const data = countries.value.slice(start, end);

  return {
    totalCount,
    currentPage,
    rowPerPage,
    pages,
    data,
  };
};

const handlePageChange = (page) => (currentPage.value = page);

async function showCountryDetail(name) {
  const { data } = await useFetch(
    `https://restcountries.com/v3.1/name/${name}`
  );
  country.value = data.value[0];
  isDisplayed.value = true;
}

function backToFirstPage() {
  if (currentPage.value > 1) {
    currentPage.value = 1;
  }
}

function goToPreviousPage() {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
}

function goToNextPage() {
  if (currentPage.value < paginationData.value.pages.length) {
    if (currentPage.value) currentPage.value++;
  }
}

function goToLastPage() {
  if (currentPage.value < paginationData.value.pages.length) {
    currentPage.value = paginationData.value.pages.length;
  }
}
</script>

<style scoped>
.pagination {
  @apply flex justify-center;
}

.pagination li {
  @apply cursor-pointer rounded-lg py-2 px-4 border border-gray-300 mr-1;
}

.pagination li.active {
  border-radius: 0.5rem;
  background-color: #6b7280;
  color: white;
}

.pagination li:hover {
  @apply bg-gray-300;
}
</style>
