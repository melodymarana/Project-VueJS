<template>
  <div id="member-table">
    <h1 class="title">{{ title }}</h1>
    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Email</th>
            <th>Phone number</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="member in members" :key="member.id">
            <td>{{ member.id }}</td>
            <td>{{ member.name }}</td>
            <td>{{ member.email }}</td>
            <td>{{ member.phonenumber }}</td>
            <td>
              <button
                @click="$emit('delete:member', member.id)"
                class="btn delete"
              >
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <p v-if="members.length < 1" class="empty">No members</p>
  </div>
</template>

<script>
export default {
  name: 'member-table',
  props: {
    members: Array,
  },
  data() {
    return {
      title: 'Members Table',
    }
  },
}
</script>

<style lang="scss">
@import '@/assets/styles/components/table.scss';
</style>
