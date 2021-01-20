<template>
  <div id="app" class="main">
    <member-form @add:member="addMember" class="mb-4" />
    <member-table
      :members="members"
      @delete:member="deleteMember"
      @edit:member="editMember"
    />
  </div>
</template>

<script>
import MemberTable from '@/components/MemberTable'
import MemberForm from '@/components/MemberForm'

export default {
  name: 'App',
  components: {
    MemberTable,
    MemberForm,
  },
  data() {
    return {
      members: [
        {
          id: 1,
          name: 'Melody Marana',
          email: 'melody@gmail.com',
          phonenumber: '0912224456',
        },
        {
          id: 2,
          name: 'Tuner Scottish',
          email: 'tuner.scott@gmail.com',
          phonenumber: '0912224457',
        },
        {
          id: 3,
          name: 'Capo Scottish',
          email: 'capo.scott@gmail.com',
          phonenumber: '0912224458',
        },
      ],
    }
  },
  methods: {
    addMember(member) {
      const lastId =
        this.members.length > 0 ? this.members[this.members.length - 1].id : 0
      const id = lastId + 1
      const newMember = { ...member, id }
      this.members = [...this.members, newMember]
      console.log(this.members)
    },
    deleteMember(id) {
      this.members = this.members.filter((member) => member.id !== id)
    },
    editMember(id, updatedMember) {
      this.members = this.members.map((member) =>
        member.id === id ? updatedMember : member
      )
    },
  },
}
</script>

<style lang="scss">
.main {
  @apply max-w-5xl mx-auto p-4 font-sans;
}

.title {
  @apply text-xl font-bold mb-4;
}
</style>
