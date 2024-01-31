<script setup>
import SearchIcon from './components/icons/SearchIcon.vue'
import groups from '../data/groups.json'
import { ref } from 'vue'
const numMembers = ref(0)
const newGroup = ref({
  section: '',
  groupName: '',
  repo: '',
  members: []
})

const addNewMembers = () => {
  newGroup.value.members = []
  for (let index = 0; index < numMembers.value; index++) {
    newGroup.value.members.push({
      projectCo: false,
      studentId: '',
      studentName: ''
    })
  }
}
const saveNewMember = () => {
  console.log(newGroup.value)
}

const addMode = ref(false)
</script>

<template>
  <div class="w-full">
    <header>
      <section
        class="flex items-center p-2 bg-gradient-to-r from-violet-500 to-fuchsia-500"
      >
        <img src="./assets/vue-icon.png" class="h-14" />
        <div>
          <h1 class="text-white text-4xl">Creative Projects</h1>
          <h2 class="italic text-indigo-200 text-xl">Play and Learn</h2>
        </div>
      </section>
    </header>
    <div
      v-show="addMode"
      class="w-full min-h-screen p-3 bg-slate-50 flex flex-col gap-2"
    >
      <div>
        Section:
        <select v-model.number="newGroup.section">
          <option value="1">1</option>
          <option value="2">2</option>
        </select>
        {{ newGroup.section }}
      </div>
      <div>
        Group Name:
        <input
          type="text"
          v-model.trim="newGroup.groupName"
          class="border border-gray-300 rounded-lg"
        />
        {{ newGroup.groupName }}
      </div>
      <div>
        GitHub Repository:
        <input
          type="text"
          v-model.trim="newGroup.repo"
          class="w-1/2 border border-gray-300 rounded-lg"
        />
        {{ newGroup.repo }}
      </div>

      <div>
        Number of Members:
        <input
          @change="addNewMembers"
          type="number"
          v-model="numMembers"
          min="0"
          class="border border-gray-300 rounded-lg"
        />
        {{ numMembers }}
      </div>

      <div
        class="flex flex-row gap-2 pt-2"
        v-for="(member, index) in newGroup.members"
        :key="index"
      >
        <div>
          <input v-model="member.projectCo" type="checkbox" />[Project
          Coordinator]
          {{ member.projectCo }}
        </div>
        <div>
          Student Id:
          <input
            v-model.number="member.studentId"
            type="text"
            class="border border-gray-300 rounded-lg outline-none"
          />
          {{ member.studentId }}
        </div>
        <div>
          Student Name:
          <input
            v-model.trim="member.studentName"
            type="text"
            class="border border-gray-300 rounded-lg outline-none"
          />
          {{ member.studentName }}
        </div>
      </div>
      <div class="flex justify-center gap-2">
        <button
          id="save-btn"
          v-on:click="saveNewMember"
          class="bg-indigo-700 text-white px-2 py-1 rounded-lg"
        >
          OK
        </button>
        <button
          @click="addMode = false"
          class="bg-red-600 text-white px-2 py-1 rounded-lg"
        >
          Cancel
        </button>
      </div>
    </div>

    <main class="p-5">
      <section class="flex justify-between pt-2 items-center">
        <div
          @click="addMode = true"
          class="text-cyan-600 hover:text-purple-500 cursor-pointer text-lg"
        >
          + Add New Group
        </div>
        <div
          class="w-1/4 flex items-center gap-3 border border-gray-300 p-1 rounded-lg"
        >
          <SearchIcon />
          <input
            class="outline-none"
            type="text"
            placeholder="type your keyword..."
          />
        </div>
      </section>
      <section>
        <div class="grid grid-cols-12 gap-2 font-semibold text-xl pb-3">
          <h3>Section</h3>
          <h3 class="col-span-2">Group Name</h3>
          <h3 class="col-span-5">GitHub Repository</h3>
          <h3 class="col-span-4">Members</h3>
        </div>
        <div
          v-for="(group, index) in groups"
          :key="group.ID"
          class="grid grid-cols-12 gap-2"
          :class="index % 2 === 0 ? 'bg-slate-100' : ''"
        >
          <p>{{ group.section }}</p>
          <p class="col-span-2">{{ group.groupName }}</p>
          <p class="col-span-5">{{ group.repo }}</p>

          <ul class="col-span-4 list-disc list-inside">
            <li
              v-for="{ studentId, studentName } in group.members"
              :key="studentId"
            >
              {{ `${studentId}  ${studentName}` }}
            </li>
          </ul>
        </div>
      </section>
    </main>
  </div>
</template>

<style scoped></style>
