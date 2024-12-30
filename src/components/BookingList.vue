<template>
  <template v-if="error">
    <ErrorCard :retry="fetchBookings"
      >There was a problem getting your bookings. Please try again later.</ErrorCard
    >
  </template>

  <template v-else>
    <section class="grid grid-flow-row gap-4">
      <template v-if="!loading">
        <BookingItem
          v-for="booking in bookings"
          :key="booking.id"
          :status="booking.status"
          @cancelled="cancelBooking(booking.id)"
          >{{ booking.eventTitle }}</BookingItem
        >
      </template>
      <template v-else>
        <LoadingEventBooking />
      </template>
    </section>
  </template>
</template>

<script setup>
import { onMounted } from 'vue';
import BookingItem from './BookingItem.vue';
import LoadingEventBooking from './LoadingEventBooking.vue';
import useBookings from '@/composables/useBookings';
import ErrorCard from './ErrorCard.vue';

const { bookings, loading, fetchBookings, cancelBooking, error } = useBookings();

onMounted(() => {
  fetchBookings();
});
</script>
