<script setup lang="ts">
import { toTypedSchema } from '@vee-validate/zod';
import { push } from 'notivue';
import { useForm } from 'vee-validate';
import { isValidPhoneNumber } from 'libphonenumber-js';
import { z } from 'zod';
import { Icon } from '@iconify/vue';
import type { ContactMessage, SuccessResponse } from '~/types/api';
import { normalizeApiError, notifyApiFailure, pickFormErrors } from '~/utils/api-errors';

type ContactFormValues = Omit<ContactMessage, 'companyName' | 'serviceInterest'> & {
  companyName: string;
  serviceInterest: string;
};

const contactFields = [
  'firstName',
  'lastName',
  'email',
  'phone',
  'companyName',
  'serviceInterest',
  'message',
] as const satisfies readonly (keyof ContactFormValues)[];

useSeoMeta({
  title: 'Contact Us | Deagensie',
  description:
    "Let's build something extraordinary. Whether you're launching a startup, scaling a growing business, or searching for exceptional creative talent, Deagensie is your trusted growth partner.",
});

const schema = toTypedSchema(
  z.object({
    firstName: z.string().min(1, 'First name is required'),
    lastName: z.string().min(1, 'Last name is required'),
    email: z.email('Enter a valid email'),
    phone: z
      .string()
      .min(1, 'Phone number is required')
      .refine(isValidPhoneNumber, 'Invalid phone number'),
    companyName: z.string().optional(),
    serviceInterest: z.string().optional(),
    message: z.string().min(10, 'Message too short'),
  })
);

const { $api } = useNuxtApp();

const { defineField, errors, handleSubmit, isSubmitting, meta, resetForm } =
  useForm<ContactFormValues>({
    validationSchema: schema,
    initialValues: {
      firstName: '',
      lastName: '',
      email: '',
      phone: '',
      companyName: '',
      serviceInterest: '',
      message: '',
    },
  });

const [firstName, firstNameAttrs] = defineField('firstName');
const [lastName, lastNameAttrs] = defineField('lastName');
const [email, emailAttrs] = defineField('email');
const [companyName, companyNameAttrs] = defineField('companyName');
const [serviceInterest, serviceInterestAttrs] = defineField('serviceInterest');
const [message, messageAttrs] = defineField('message');

const isSubmitDisabled = computed(() => isSubmitting.value || !meta.value.valid);

const onSubmit = handleSubmit(async (values, actions) => {
  try {
    await $api<SuccessResponse>('/contact', {
      method: 'POST',
      body: values,
    });

    resetForm();
    push.success({
      title: 'Message sent',
      message: "Thanks. We'll get back to you within 24 hours.",
    });
  } catch (error: unknown) {
    const failure = normalizeApiError(error);
    actions.setErrors(pickFormErrors(failure.fieldErrors, contactFields));
    notifyApiFailure(failure);
  }
});
</script>

<template>
  <div class="min-h-screen bg-white">
    <!-- Andela-Style Editorial Header -->
    <section class="border-b border-gray-100 bg-[#FCFCFE] pt-28 pb-16 lg:pt-36 lg:pb-20">
      <div v-reveal="'fade-up'" class="mx-auto w-5/6 max-w-7xl space-y-5 text-center">
        <span
          class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
        >
          Let&apos;s Connect
        </span>
        <h1 class="type-feature-title font-serif text-gray-900">
          Let&apos;s Build Something <br class="hidden sm:inline" />
          <span class="text-[#04308F]">Extraordinary.</span>
        </h1>
        <p
          class="font-open-sans mx-auto max-w-3xl text-base leading-relaxed font-normal text-gray-600 sm:text-lg"
        >
          Whether you&apos;re launching a startup, scaling a growing business, building a global
          brand, or searching for exceptional creative talent, Deagensie is your trusted growth
          partner.
        </p>
      </div>
    </section>

    <!-- Contact Form + Info Panel -->
    <section class="py-16 lg:py-24">
      <div class="mx-auto w-5/6 max-w-7xl lg:flex lg:items-start lg:gap-14">
        <!-- Left Info Panel -->
        <div class="mb-12 space-y-6 lg:mb-0 lg:w-[420px] lg:shrink-0">
          <!-- Offices / Locations Card -->
          <div
            class="space-y-5 rounded-3xl border border-gray-100 bg-gray-50/80 p-6 shadow-xs sm:p-7"
          >
            <div class="flex items-center justify-between border-b border-gray-200/60 pb-3.5">
              <p class="font-serif text-lg font-normal text-gray-900">Our Locations</p>
              <span
                class="rounded-full bg-emerald-50 px-2.5 py-0.5 text-[11px] font-semibold text-emerald-700"
              >
                Lagos, Nigeria
              </span>
            </div>

            <div class="space-y-3.5">
              <!-- Admin HQ -->
              <div
                class="group rounded-2xl border border-gray-100 bg-white p-4.5 shadow-2xs transition-all duration-200 hover:border-[#04308F]/30 hover:shadow-sm"
              >
                <div class="flex items-start gap-3.5">
                  <div
                    class="flex size-10 shrink-0 items-center justify-center rounded-xl bg-[#04308F]/10 text-[#04308F]"
                  >
                    <Icon icon="lucide:building-2" class="size-5" />
                  </div>
                  <div class="space-y-1">
                    <div class="flex items-center gap-2">
                      <span
                        class="font-mono text-xs font-bold tracking-wider text-[#04308F] uppercase"
                      >
                        Admin HQ
                      </span>
                      <span
                        class="rounded bg-gray-100 px-1.5 py-0.5 text-[10px] font-medium text-gray-600"
                      >
                        VI
                      </span>
                    </div>
                    <p class="text-sm font-bold text-gray-900">2A Louis Solomon Close</p>
                    <p class="text-xs leading-relaxed text-gray-500">
                      Off Ahmadu Bello Way, Victoria Island, Lagos
                    </p>
                  </div>
                </div>
              </div>

              <!-- Operations -->
              <div
                class="group rounded-2xl border border-gray-100 bg-white p-4.5 shadow-2xs transition-all duration-200 hover:border-[#026662]/30 hover:shadow-sm"
              >
                <div class="flex items-start gap-3.5">
                  <div
                    class="flex size-10 shrink-0 items-center justify-center rounded-xl bg-[#026662]/10 text-[#026662]"
                  >
                    <Icon icon="lucide:map-pin" class="size-5" />
                  </div>
                  <div class="space-y-1">
                    <div class="flex items-center gap-2">
                      <span
                        class="font-mono text-xs font-bold tracking-wider text-[#026662] uppercase"
                      >
                        Operations
                      </span>
                      <span
                        class="rounded bg-gray-100 px-1.5 py-0.5 text-[10px] font-medium text-gray-600"
                      >
                        VGC
                      </span>
                    </div>
                    <p class="text-sm font-bold text-gray-900">Suite J256, Road 5</p>
                    <p class="text-xs leading-relaxed text-gray-500">
                      Ikota Business Complex, Victoria Garden City, Lagos
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Direct Channels Card -->
          <div
            class="space-y-4 rounded-3xl border border-gray-100 bg-gray-50/80 p-6 shadow-xs sm:p-7"
          >
            <p class="font-serif text-lg font-normal text-gray-900">Direct Inquiries</p>
            <ul class="space-y-4">
              <!-- Email -->
              <li class="flex items-center gap-3.5">
                <div
                  class="flex size-10 shrink-0 items-center justify-center rounded-xl bg-[#04308F]/10 text-[#04308F]"
                >
                  <Icon icon="hugeicons:mail-02" class="size-5" />
                </div>
                <div class="min-w-0 flex-1">
                  <p class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">Email</p>
                  <a
                    href="mailto:hello@deagensie.com"
                    class="truncate text-sm font-semibold text-gray-900 transition-colors hover:text-[#04308F] hover:underline"
                  >
                    hello@deagensie.com
                  </a>
                </div>
              </li>

              <!-- Website -->
              <li class="flex items-center gap-3.5">
                <div
                  class="flex size-10 shrink-0 items-center justify-center rounded-xl bg-[#05DED5]/15 text-[#026662]"
                >
                  <Icon icon="lucide:globe" class="size-5" />
                </div>
                <div class="min-w-0 flex-1">
                  <p class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">
                    Website
                  </p>
                  <a
                    href="https://www.deagensie.com"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="truncate text-sm font-semibold text-gray-900 transition-colors hover:text-[#04308F] hover:underline"
                  >
                    www.deagensie.com
                  </a>
                </div>
              </li>

              <!-- Phone -->
              <li class="flex items-center gap-3.5">
                <div
                  class="flex size-10 shrink-0 items-center justify-center rounded-xl bg-gray-200/60 text-gray-700"
                >
                  <Icon icon="hugeicons:call-02" class="size-5" />
                </div>
                <div class="min-w-0 flex-1">
                  <p class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">Phone</p>
                  <a
                    href="tel:+2348063836398"
                    class="truncate text-sm font-semibold text-gray-900 transition-colors hover:text-[#04308F] hover:underline"
                  >
                    +234 806 383 6398
                  </a>
                </div>
              </li>
            </ul>
          </div>

          <!-- Social Media Card -->
          <div
            class="space-y-4 rounded-3xl border border-gray-100 bg-gray-50/80 p-6 shadow-xs sm:p-7"
          >
            <div class="flex items-center justify-between">
              <div>
                <p class="font-serif text-lg font-normal text-gray-900">Social Media</p>
                <p class="text-xs text-gray-500">Connect with the community</p>
              </div>
              <span
                class="rounded-full bg-[#04308F]/10 px-2.5 py-1 font-mono text-xs font-semibold text-[#04308F]"
              >
                @deagensie
              </span>
            </div>

            <div class="grid grid-cols-2 gap-2.5 pt-1">
              <!-- Instagram -->
              <a
                href="https://instagram.com/deagensie"
                target="_blank"
                rel="noopener noreferrer"
                class="flex items-center gap-2.5 rounded-xl border border-gray-200/80 bg-white px-3.5 py-2.5 text-gray-700 transition-all duration-200 hover:border-[#8F039C] hover:text-[#8F039C] hover:shadow-xs"
              >
                <Icon icon="ri:instagram-line" class="size-4 shrink-0 text-[#8F039C]" />
                <span class="text-xs font-semibold">Instagram</span>
              </a>

              <!-- LinkedIn -->
              <a
                href="https://linkedin.com/company/deagensie"
                target="_blank"
                rel="noopener noreferrer"
                class="flex items-center gap-2.5 rounded-xl border border-gray-200/80 bg-white px-3.5 py-2.5 text-gray-700 transition-all duration-200 hover:border-[#04308F] hover:text-[#04308F] hover:shadow-xs"
              >
                <Icon icon="mingcute:linkedin-fill" class="size-4 shrink-0 text-[#0077B5]" />
                <span class="text-xs font-semibold">LinkedIn</span>
              </a>

              <!-- TikTok -->
              <a
                href="https://tiktok.com/@deagensie"
                target="_blank"
                rel="noopener noreferrer"
                class="flex items-center gap-2.5 rounded-xl border border-gray-200/80 bg-white px-3.5 py-2.5 text-gray-700 transition-all duration-200 hover:border-gray-900 hover:text-gray-900 hover:shadow-xs"
              >
                <Icon icon="ri:tiktok-fill" class="size-4 shrink-0 text-gray-900" />
                <span class="text-xs font-semibold">TikTok</span>
              </a>

              <!-- X (Twitter) -->
              <a
                href="https://x.com/deagensie"
                target="_blank"
                rel="noopener noreferrer"
                class="flex items-center gap-2.5 rounded-xl border border-gray-200/80 bg-white px-3.5 py-2.5 text-gray-700 transition-all duration-200 hover:border-gray-900 hover:text-gray-900 hover:shadow-xs"
              >
                <Icon icon="devicon:twitter" class="size-4 shrink-0 text-gray-900" />
                <span class="text-xs font-semibold">X (Twitter)</span>
              </a>
            </div>
          </div>
        </div>

        <!-- Right Form Panel -->
        <form
          class="flex-1 space-y-8 rounded-3xl border border-gray-100 bg-white p-8 shadow-md shadow-gray-100/60 lg:p-12"
          @submit="onSubmit"
        >
          <FieldSet>
            <FieldLegend class="mb-1 font-serif text-xl font-normal text-gray-900"
              >Send us a message</FieldLegend
            >
            <FieldDescription class="text-sm leading-relaxed text-gray-500">
              Fill out the form below and we&apos;ll get back to you within 24 hours.
            </FieldDescription>

            <FieldGroup class="mt-8 space-y-6">
              <div class="grid gap-5 lg:grid-cols-2">
                <Field :data-invalid="!!errors.firstName">
                  <FieldLabel for="firstName" class="text-sm font-semibold text-gray-700"
                    >First Name</FieldLabel
                  >
                  <Input
                    id="firstName"
                    v-model="firstName"
                    v-bind="firstNameAttrs"
                    placeholder="e.g. John"
                    class="mt-1.5 rounded-xl border-gray-200"
                  />
                  <FieldError v-if="errors.firstName" class="mt-1 text-xs text-red-500">{{
                    errors.firstName
                  }}</FieldError>
                </Field>

                <Field :data-invalid="!!errors.lastName">
                  <FieldLabel for="lastName" class="text-sm font-semibold text-gray-700"
                    >Last Name</FieldLabel
                  >
                  <Input
                    id="lastName"
                    v-model="lastName"
                    v-bind="lastNameAttrs"
                    placeholder="e.g. Doe"
                    class="mt-1.5 rounded-xl border-gray-200"
                  />
                  <FieldError v-if="errors.lastName" class="mt-1 text-xs text-red-500">{{
                    errors.lastName
                  }}</FieldError>
                </Field>
              </div>

              <div class="grid gap-5 lg:grid-cols-2">
                <Field :data-invalid="!!errors.email">
                  <FieldLabel for="email" class="text-sm font-semibold text-gray-700"
                    >Email Address</FieldLabel
                  >
                  <Input
                    id="email"
                    v-model="email"
                    type="email"
                    v-bind="emailAttrs"
                    placeholder="hello@company.com"
                    class="mt-1.5 rounded-xl border-gray-200"
                  />
                  <FieldError v-if="errors.email" class="mt-1 text-xs text-red-500">{{
                    errors.email
                  }}</FieldError>
                </Field>

                <Field :data-invalid="!!errors.phone">
                  <FieldLabel for="phone" class="text-sm font-semibold text-gray-700"
                    >Phone Number</FieldLabel
                  >
                  <PhoneInput id="phone" name="phone" class="mt-1.5" />
                  <FieldError v-if="errors.phone" class="mt-1 text-xs text-red-500">{{
                    errors.phone
                  }}</FieldError>
                </Field>
              </div>

              <Field :data-invalid="!!errors.companyName">
                <FieldLabel for="company" class="text-sm font-semibold text-gray-700">
                  Company Name <span class="font-normal text-gray-400">(optional)</span>
                </FieldLabel>
                <Input
                  id="company"
                  v-model="companyName"
                  v-bind="companyNameAttrs"
                  placeholder="Acme Inc."
                  class="mt-1.5 rounded-xl border-gray-200"
                />
                <FieldError v-if="errors.companyName" class="mt-1 text-xs text-red-500">{{
                  errors.companyName
                }}</FieldError>
              </Field>

              <Field :data-invalid="!!errors.serviceInterest">
                <FieldLabel class="text-sm font-semibold text-gray-700">
                  Service Interest <span class="font-normal text-gray-400">(optional)</span>
                </FieldLabel>
                <PagesContactServiceInterestCombobox
                  v-model="serviceInterest"
                  v-bind="serviceInterestAttrs"
                  class="mt-1.5"
                />
                <FieldError v-if="errors.serviceInterest" class="mt-1 text-xs text-red-500">{{
                  errors.serviceInterest
                }}</FieldError>
              </Field>

              <Field :data-invalid="!!errors.message">
                <FieldLabel for="message" class="text-sm font-semibold text-gray-700"
                  >Message</FieldLabel
                >
                <Textarea
                  id="message"
                  v-model="message"
                  v-bind="messageAttrs"
                  placeholder="Tell us about your project, goals, or challenges..."
                  :rows="5"
                  class="mt-1.5 rounded-xl border-gray-200"
                />
                <FieldError v-if="errors.message" class="mt-1 text-xs text-red-500">{{
                  errors.message
                }}</FieldError>
              </Field>
            </FieldGroup>
          </FieldSet>

          <button
            type="submit"
            :disabled="isSubmitDisabled"
            class="flex w-full items-center justify-center gap-2 rounded-full bg-[#04308F] px-8 py-4 text-base font-semibold text-white shadow-md transition-all duration-300 hover:scale-105 hover:bg-[#05DED5] hover:text-gray-900 disabled:cursor-not-allowed disabled:opacity-50"
          >
            <template v-if="isSubmitting">
              Sending
              <Icon icon="svg-spinners:3-dots-fade" class="mb-[-0.25lh]" />
            </template>
            <template v-else>
              Send Message
              <Icon icon="lucide:send" class="text-base" />
            </template>
          </button>
        </form>
      </div>
    </section>
  </div>
</template>

<style scoped lang="css"></style>
