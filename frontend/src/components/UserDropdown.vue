<template>
  <Dropdown
    :options="[
      /* {
        icon: 'settings',
        label: 'Settings',
        onClick: () => (showSettings = true),
      }, */
      {
        icon: 'log-out',
        label: 'Log out',
        onClick: () => logout(),
      },
    ]">
    <template v-slot="{ open }">
      <button
        class="flex w-[15rem] items-center rounded-md px-2 py-2 text-left"
        :class="open ? 'bg-white shadow-sm' : 'hover:bg-gray-200'">
        <FrappeDriveLogo class="w-8 h-8 rounded" />
        <div class="ml-2 flex flex-col">
          <div class="text-base font-medium text-gray-900 leading-none">
            Frappe Drive
          </div>
          <div class="mt-1 hidden text-sm text-gray-700 sm:inline leading-none">
            {{ fullName }}
          </div>
        </div>
        <FeatherIcon
          name="chevron-down"
          class="ml-auto hidden h-4 w-4 sm:inline" />
      </button>
    </template>
  </Dropdown>
  <Settings v-if="showSettings" v-model="showSettings" />
</template>
<script>
import { Dropdown, FeatherIcon, Avatar } from "frappe-ui";
import Settings from "@/components/Settings.vue";
import FrappeDriveLogo from "@/components/FrappeDriveLogo.vue";

export default {
  name: "UserDropdown",
  components: {
    Dropdown,
    FeatherIcon,
    Avatar,
    Settings,
    FrappeDriveLogo,
  },
  data: () => ({
    showSettings: false,
  }),
  methods: {
    logout() {
      this.$store.dispatch("logout");
    },
  },
  computed: {
    firstName() {
      return this.$store.state.user.fullName.split(" ");
    },
    fullName() {
      return this.$store.state.user.fullName;
    },
    imageURL() {
      return this.$store.state.user.imageURL;
    },
  },
};
</script>
