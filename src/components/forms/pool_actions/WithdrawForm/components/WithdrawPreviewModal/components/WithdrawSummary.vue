<script setup lang="ts">
import useNumbers, { FNumFormats } from '@/composables/useNumbers';
import { useUserSettings } from '@/providers/user-settings.provider';
import { Pool } from '@/services/pool/types';

/**
 * TYPES
 */
type Props = {
  pool: Pool;
  fiatTotal: string;
  priceImpact: number;
};

/**
 * PROPS & EMITS
 */
defineProps<Props>();

/**
 * COMPOSABLES
 */
const { fNum2 } = useNumbers();
const { currency } = useUserSettings();
</script>

<template>
  <div class="summary-table">
    <h6 class="p-2">
      {{ $t('summary') }}
    </h6>
    <div class="flex flex-col py-2">
      <div class="summary-table-row">
        <div class="summary-table-label">
          {{ $t('total') }}
        </div>
        <div class="summary-table-number">
          {{ fNum2(fiatTotal, FNumFormats.fiat) }}
          <BalTooltip
            :text="$t('tooltips.withdraw.total', [currency.toUpperCase()])"
            iconSize="sm"
            class="ml-2"
          />
        </div>
      </div>
      <div class="summary-table-row">
        <div class="summary-table-label">
          {{ $t('priceImpact') }}
        </div>
        <div class="summary-table-number">
          {{ fNum2(priceImpact, FNumFormats.percent) }}
          <BalTooltip
            :text="$t('tooltips.withdraw.priceImpact')"
            iconSize="sm"
            width="72"
            class="ml-2"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.summary-table {
  @apply border dark:border-gray-700 divide-y dark:divide-gray-700 rounded-lg mt-4;
}

.summary-table-row {
  @apply grid grid-cols-2 px-2 py-1;
}

.summary-table-label {
  @apply flex items-center;
}

.summary-table-number {
  @apply flex items-center justify-end;
}
</style>
