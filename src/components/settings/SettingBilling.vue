<script setup lang="ts">
import { ref } from "vue";

const billing = ref({
  plan: "professional",
  monthlyPrice: 29.99,
  renewalDate: "July 18, 2026",
  paymentMethod: "Visa ending in 4242",
  invoices: [
    { id: 1, date: "June 18, 2026", amount: "$29.99", status: "Paid" },
    { id: 2, date: "May 18, 2026", amount: "$29.99", status: "Paid" },
    { id: 3, date: "April 18, 2026", amount: "$29.99", status: "Paid" },
  ],
});

const plans = [
  {
    name: "starter",
    label: "Starter",
    price: 9.99,
    features: ["Up to 3 platforms", "Basic analytics", "Email support"],
  },
  {
    name: "professional",
    label: "Professional",
    price: 29.99,
    features: ["Up to 10 platforms", "Advanced analytics", "Priority support"],
  },
  {
    name: "enterprise",
    label: "Enterprise",
    price: 99.99,
    features: [
      "Unlimited platforms",
      "Custom analytics",
      "24/7 dedicated support",
    ],
  },
];

function downloadInvoice(invoiceId: number) {
  alert(`Downloading invoice #${invoiceId}...`);
}
</script>

<template>
  <div class="billing-settings">
    <h2>Billing & Subscription</h2>

    <div class="setting-card">
      <h3>Current Plan</h3>
      <div class="current-plan">
        <div class="plan-details">
          <h4>
            {{
              billing.plan.charAt(0).toUpperCase() + billing.plan.slice(1)
            }}
            Plan
          </h4>
          <p class="plan-price">${{ billing.monthlyPrice }}/month</p>
          <p class="plan-renewal">Renews on {{ billing.renewalDate }}</p>
        </div>
        <div class="plan-actions">
          <button class="btn-secondary">Change Plan</button>
          <button class="btn-danger">Cancel Subscription</button>
        </div>
      </div>
    </div>

    <div class="setting-card">
      <h3>Payment Method</h3>
      <div class="payment-method">
        <div class="method-display">
          <span class="method-icon">💳</span>
          <div>
            <p class="method-name">{{ billing.paymentMethod }}</p>
            <p class="method-date">Expires 12/2028</p>
          </div>
        </div>
        <button class="btn-secondary">Update Payment</button>
      </div>
    </div>

    <div class="setting-card">
      <h3>Available Plans</h3>
      <div class="plans-grid">
        <div
          v-for="plan in plans"
          :key="plan.name"
          class="plan-card"
          :class="{ active: billing.plan === plan.name }"
        >
          <h4>{{ plan.label }}</h4>
          <p class="plan-price">${{ plan.price }}/mo</p>
          <ul class="plan-features">
            <li v-for="feature in plan.features" :key="feature">
              ✓ {{ feature }}
            </li>
          </ul>
          <button
            :class="billing.plan === plan.name ? 'btn-active' : 'btn-upgrade'"
          >
            {{ billing.plan === plan.name ? "Current Plan" : "Upgrade" }}
          </button>
        </div>
      </div>
    </div>

    <div class="setting-card">
      <h3>Invoices</h3>
      <div class="invoices-table">
        <div class="invoice-header">
          <span class="col-date">Date</span>
          <span class="col-amount">Amount</span>
          <span class="col-status">Status</span>
          <span class="col-action">Action</span>
        </div>
        <div
          v-for="invoice in billing.invoices"
          :key="invoice.id"
          class="invoice-row"
        >
          <span class="col-date">{{ invoice.date }}</span>
          <span class="col-amount">{{ invoice.amount }}</span>
          <span class="col-status">
            <span class="status-badge paid">{{ invoice.status }}</span>
          </span>
          <span class="col-action">
            <button class="btn-small" @click="downloadInvoice(invoice.id)">
              📥 Download
            </button>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.billing-settings {
  display: flex;
  flex-direction: column;
  gap: 32px;
}

h2 {
  font-size: 24px;
  margin: 0 0 16px 0;
}

.setting-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 24px;
}

.setting-card h3 {
  font-size: 16px;
  margin: 0 0 20px 0;
}

.current-plan {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 24px;
  padding: 20px;
  background: var(--bg);
  border-radius: 8px;
}

.plan-details h4 {
  font-size: 18px;
  margin: 0 0 8px 0;
}

.plan-price {
  font-size: 24px;
  font-weight: 600;
  color: var(--accent);
  margin: 0;
}

.plan-renewal {
  font-size: 12px;
  color: var(--text-muted);
  margin: 8px 0 0 0;
}

.plan-actions {
  display: flex;
  gap: 12px;
}

.payment-method {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background: var(--bg);
  border-radius: 8px;
  gap: 16px;
}

.method-display {
  display: flex;
  align-items: center;
  gap: 12px;
}

.method-icon {
  font-size: 28px;
}

.method-name {
  font-size: 14px;
  font-weight: 500;
  margin: 0;
}

.method-date {
  font-size: 12px;
  color: var(--text-muted);
  margin: 4px 0 0 0;
}

.plans-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 16px;
}

.plan-card {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 16px;
  transition: all 0.2s;
}

.plan-card:hover {
  border-color: var(--accent);
}

.plan-card.active {
  background: var(--glow-purple);
  border-color: var(--accent);
}

.plan-card h4 {
  font-size: 16px;
  margin: 0;
}

.plan-features {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
  flex: 1;
}

.plan-features li {
  font-size: 12px;
  color: var(--text-muted);
}

.btn-active,
.btn-upgrade {
  background: var(--accent);
  color: #fff;
  border: none;
  padding: 10px 16px;
  border-radius: 6px;
  font-size: 13px;
  cursor: pointer;
  transition: opacity 0.2s;
}

.btn-active {
  opacity: 0.6;
  cursor: default;
}

.btn-upgrade:hover {
  opacity: 0.88;
}

.invoices-table {
  background: var(--bg);
  border-radius: 8px;
  overflow: hidden;
}

.invoice-header,
.invoice-row {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  gap: 16px;
  padding: 12px 16px;
  align-items: center;
}

.invoice-header {
  background: var(--bg-hover);
  font-weight: 600;
  font-size: 12px;
  text-transform: uppercase;
  color: var(--text-muted);
}

.invoice-row {
  border-top: 1px solid var(--border);
  font-size: 14px;
}

.invoice-row:hover {
  background: var(--bg-hover);
}

.col-date {
  color: var(--text-h);
}

.col-amount {
  color: var(--accent);
  font-weight: 500;
}

.status-badge {
  display: inline-block;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 11px;
  font-weight: 600;
}

.status-badge.paid {
  background: rgba(67, 233, 123, 0.1);
  color: var(--accent-4);
}

.btn-small {
  background: var(--bg);
  border: 1px solid var(--border);
  color: var(--text);
  padding: 6px 12px;
  border-radius: 4px;
  font-size: 12px;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-small:hover {
  border-color: var(--accent);
  color: var(--text-h);
}

.btn-secondary,
.btn-danger {
  background: var(--bg-hover);
  border: 1px solid var(--border);
  color: var(--text);
  padding: 10px 16px;
  border-radius: 6px;
  font-size: 13px;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-secondary:hover {
  border-color: var(--accent);
}

.btn-danger {
  background: rgba(255, 107, 107, 0.1);
  border-color: rgba(255, 107, 107, 0.3);
  color: #ff6b6b;
}

.btn-danger:hover {
  background: rgba(255, 107, 107, 0.2);
}

@media (max-width: 768px) {
  .current-plan {
    flex-direction: column;
  }

  .plans-grid {
    grid-template-columns: 1fr;
  }

  .invoice-header,
  .invoice-row {
    grid-template-columns: 1fr;
    gap: 8px;
  }

  .col-date::before {
    content: "Date: ";
    font-weight: 600;
  }

  .col-amount::before {
    content: "Amount: ";
    font-weight: 600;
  }

  .col-status::before {
    content: "Status: ";
    font-weight: 600;
  }

  .col-action::before {
    content: "Action: ";
    font-weight: 600;
  }
}
</style>
