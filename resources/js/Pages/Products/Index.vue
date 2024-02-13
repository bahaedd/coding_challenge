<script setup>
import BreezeAuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, useForm  } from '@inertiajs/inertia-vue3';
import { Table } from "@protonemedia/inertiajs-tables-laravel-query-builder";

defineProps(["products"]);
const form = useForm({});

function destroy(id) {
    if (confirm("Are you sure ?")) {
        form.delete(route('products.destroy', id));
    }
}
</script>

<template>
    <Head title="Dashboard" />

    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Products
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                         <Table :resource="products">
                            <template #cell(actions)="{ item: product }">
                            <a :href="route('products.edit', product.id)" className="mx-2 px-4 py-2 text-sm text-white bg-blue-500 rounded">
                                Edit
                            </a>
                            <button @click="destroy(product.id)" type="button" className="mx-2 px-4 py-2 text-sm text-white bg-red-500 rounded">
                                delete
                            </button>
                            </template>
                        </Table>
                    </div>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>