<template>
  <li>

    <info
            v-if="isContactInfoVisible"
            @closeModal="closeInfoModal"
    >
      <p><b>Full Contact Name</b> {{ item.fullName}}</p>
      <p><b>Phone Number:</b> {{ item.phoneNumber }}</p>
      <p>
        <b>Group:</b>&nbsp;
        <span class="group-name" :style="groupColor">{{ groupName }}</span>
      </p>
    </info>

    <div>
      <p><b>Full Name:</b> {{ item.fullName }}</p>
      <p><b>Phone Number:</b> {{ item.phoneNumber }}</p>
      <p>
        <b>Group:</b>&nbsp;
        <span class="group-name" :style="groupColor">{{ groupName }}</span>
      </p>
    </div>
    <div class="actions">
      <button
        class="btn-mini"
        :class="{ warning: editMode }"
        @click="handleEditItem(item)"
      >
        {{ editMode ? "Cancel" : "Edit" }}
      </button>
      <button class="btn-mini danger" @click="handleDeleteItem(item)">
        Delete
      </button>
      <button
              class="btn-mini"
              @click="showInfo"
      >
        See More
      </button>
    </div>
  </li>
</template>

<script>
import { mapState, mapMutations } from "vuex";
import Info from '@/components/Info/Info'

export default {
  name: "ContactListItem",
  components: {
    Info
  },
  props: ["item"],
  data() {
    return {
      isContactInfoVisible: false
    };
  },
  computed: {
    ...mapState("contact", {
      editMode(state) {
        return state.model.id === this.item.id;
      }
    }),
    ...mapState("contactGroup", {
      contactGroups: state => state.items
    }),
    group() {
      return this.contactGroups.find(c => c.id === this.item.group);
    },
    groupName() {
      return this.group ? this.group.name : "Ungrouped";
    },
    groupColor() {
      return { background: this.group ? this.group.color : null };
    }
  },
  methods: {
    ...mapMutations("contact", ["editContact", "deleteContact"]),

    handleEditItem(item) {
      this.editContact(this.editMode ? null : item);
    },
    handleDeleteItem(item) {
      const isOkey = confirm("It will be removed? Are you sure?");

      if (isOkey) {
        this.deleteContact(item);
      }
    },
    showInfo() {
      this.isContactInfoVisible = true;
    },
    closeInfoModal() {
      this.isContactInfoVisible = false;
    }
  }
};
</script>

<style lang="scss" scoped></style>
