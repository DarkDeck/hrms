<template>
    <div class="flex flex-col mt-6">
        <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
            <div
                class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8"
            >
                <div
                    class="shadow overflow-hidden border-b bg-white border-gray-200 sm:rounded-lg"
                >
                    <div class="flex items-center justify-between mb-0">
                        <h5 class="mx-6 my-5 font-semibold font bg-white">
                            👮‍♀️ Civil Service Eligibility
                        </h5>
                        <inertia-link
                            class="h-8 text-xs items-center rounded-lg btn-indigo my-2 mx-6"
                            :href="route('employees.create')"
                        >
                            ➕ Add
                        </inertia-link>
                    </div>
                    <table class="min-w-full divide-y divide-gray-200">
                        <thead class="bg-white">
                            <tr
                                class="transition-all hover:bg-gray-100 hover:shadow-lg"
                            >
                                <th
                                    scope="col"
                                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                                >
                                    Eligibility Name
                                </th>
                                <th
                                    scope="col"
                                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                                >
                                    Rating
                                </th>
                                <th
                                    scope="col"
                                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                                >
                                    Date of Exam
                                </th>
                                <th
                                    scope="col"
                                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                                >
                                    Place of Exam
                                </th>
                                <th
                                    scope="col"
                                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                                >
                                    License Number
                                </th>
                                <th
                                    scope="col"
                                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                                >
                                    License Expiration
                                </th>
                                <th
                                    scope="col"
                                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                                >
                                    Action
                                </th>
                            </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-gray-200">
                            <tr
                                class="transition-all hover:bg-gray-100 hover:shadow-lg"
                                v-for="eligibility in eligibilities"
                                :key="eligibility.id"
                            >
                                <td class="px-6 py-4 whitespace-nowrap">
                                    <div class="text-sm text-gray-900">
                                        {{ eligibility.eligibility_name }}
                                    </div>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap">
                                    <div class="text-sm text-gray-900">
                                        {{ eligibility.eligibility_rating }}
                                    </div>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap">
                                    <div class="text-sm text-gray-900">
                                        {{
                                            eligibility.eligibility_date_of_exam
                                        }}
                                    </div>
                                </td>
                                <td
                                    class="px-6 py-4 whitespace-nowrap text-sm text-gray-500"
                                >
                                    <div class="text-sm text-gray-900">
                                        {{
                                            eligibility.eligibility_place_of_exam
                                        }}
                                    </div>
                                </td>
                                <td
                                    class="px-6 py-4 whitespace-nowrap text-sm text-gray-500"
                                >
                                    <div class="text-sm text-gray-900">
                                        {{
                                            eligibility.eligibility_license_number
                                        }}
                                    </div>
                                </td>
                                <td
                                    class="px-6 py-4 whitespace-nowrap text-sm text-gray-500"
                                >
                                    <div class="text-sm text-gray-900">
                                        {{
                                            eligibility.eligibility_license_expiration
                                        }}
                                    </div>
                                </td>
                                <td
                                    class="px-6 py-4 whitespace-nowrap text-sm font-medium"
                                >
                                    <span
                                        class="text-indigo-600 hover:text-indigo-900"
                                        >✏️ Edit</span
                                    >
                                    <span
                                        @click="
                                            destroy(
                                                eligibility.id,
                                                eligibility.eligibility_name
                                            )
                                        "
                                        class="text-red-600 inline-flex mt-2 cursor-pointer hover:text-red-900"
                                        >🗑️ Delete</span
                                    >
                                </td>
                            </tr>
                            <tr v-if="eligibilities.length === 0">
                                <td
                                    class="border-t text-red-500 text-sm px-6 py-4 font-bold"
                                    colspan="4"
                                >
                                    ☹️ No eligibility added.
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        eligibilities: Array
    },
    methods: {
        destroy(id, name) {
            swal({
                title: "Delete",
                text: `Are you sure you want to delete ${name}?`,
                buttons: true,
                dangerMode: true
            }).then(willDelete => {
                if (willDelete) {
                    this.$inertia.delete(this.route("eligibility.destroy", id));
                }
            });
        }
    }
};
</script>