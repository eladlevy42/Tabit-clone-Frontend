# Tabit Clone

Frontend for a [Tabit](https://tabitisrael.co.il/) clone: an Israeli restaurant reservation app. Guests browse restaurants, check table availability, book a table, and buy gift cards. The API lives in a separate backend.

This is the final project of a course, built as a team. This repository is [Elad Levy](https://github.com/eladlevy42)’s fork of the original project, [Oriassia/Tabit-clone-Frontend](https://github.com/Oriassia/Tabit-clone-Frontend).

**Live demo:** [https://tabit-clone.vercel.app](https://tabit-clone.vercel.app)

**Backend:** [eladlevy42/tabit-clone-back-elad](https://github.com/eladlevy42/tabit-clone-back-elad)

## Features

- **Home.** Date, time, party size, and area (around the user, Tel Aviv–Jaffa, Jerusalem, Haifa, Center, North, or South), then a jump into table search. The page also previews gift cards, deliveries, new restaurants, and nearby restaurants.
- **Restaurants.** Search by name, filter by cuisine tags and area, and scroll the results. Each card opens a details page with photos, description, menus, opening hours, address, phone, website, and social links.
- **Table availability.** Search by party size, date, and time. Results show open tables for the requested slot and the half hours before and after, with seating at the bar, inside, or outside. The list is paired with a Google Map; selecting a marker scrolls to that restaurant.
- **Reservations.** Pick a table, enter name, phone, email, and notes (the slot is held for five minutes), then confirm. The confirmation page can modify or cancel the booking.
- **Gift cards (Tabit Gift It).** Browse restaurants by category, send a card to a friend or to yourself by phone or email, confirm with an SMS code, and check out. The issued card shows a QR code that can be saved as a PDF, and a redeem link marks the card as used.
- **Deliveries and takeout.** A list-and-map browser with a delivery or takeout selector, cuisine tags, and area. The restaurant request is filtered by area, category, and name.
- **Map and places.** Google Maps markers for search results, plus Places autocomplete for adding a location. The browser’s geolocation is used when the user picks a nearby area.

## Tech stack

Verified from `package.json` and the code that imports them:

- [React](https://react.dev/) 18 and [TypeScript](https://www.typescriptlang.org/)
- [Vite](https://vitejs.dev/) 5
- [Tailwind CSS](https://tailwindcss.com/) 3
- [shadcn/ui](https://ui.shadcn.com/) on [Radix UI](https://www.radix-ui.com/), with `class-variance-authority`, `clsx`, `tailwind-merge`, and `lucide-react`
- [React Router](https://reactrouter.com/) 6
- [Axios](https://axios-http.com/)
- [Google Maps](https://github.com/JustFly1984/react-google-maps-api) (`@react-google-maps/api`) and [react-google-autocomplete](https://github.com/ErrorPro/react-google-autocomplete)
- [Framer Motion](https://www.framer.com/motion/), [date-fns](https://date-fns.org/), and [react-infinite-scroll-component](https://github.com/ankeetmaini/react-infinite-scroll-component)
- [qrcode.react](https://github.com/zpao/qrcode.react) and [jsPDF](https://github.com/parallax/jsPDF) for gift-card QR codes
- ESLint

## Project structure

```
src/
  pages/            route screens (home, restaurants, booking, gift cards)
  components/
    ui/             shadcn/ui primitives
    custom/         nav, map, reservation flow, gift cards, restaurant details
  context/          location, reservation, and layout providers
  services/         Axios client, table helpers, time formatting
  types/            restaurant, reservation, and gift-card types
  hooks/
  lib/
public/             logo assets
```

Routes are declared in `src/App.tsx`. The Axios client in `src/services/api.services.ts` chooses the API base URL from the environment variables below.

## Getting started

Requirements: Node.js and npm.

```bash
npm install
cp .env.example .env
npm run dev
```

The dev server prints a local URL (Vite’s default is `http://localhost:5173`).

### Environment variables

Copy `.env.example` to `.env` and fill in the values locally. `.env` is gitignored. Do not commit real keys.

| Name | Purpose |
| --- | --- |
| `VITE_ENV` | Set to `development` to use the dev API. Any other value uses the production API. |
| `VITE_DEV_API_BASE_URL` | Backend base URL when `VITE_ENV` is `development`. |
| `VITE_PROD_API_BASE_URL` | Backend base URL otherwise. |
| `VITE_GOOGLE_API` | Google Maps and Places API key. |

## Scripts

| Script | Command | Description |
| --- | --- | --- |
| `dev` | `vite` | Start the dev server |
| `build` | `vite build` | Production build to `dist/` |
| `preview` | `vite preview` | Serve the production build |
| `lint` | `eslint .` | Run ESLint |

The production build is a static Vite app. `vercel.json` rewrites every path to `index.html` so client-side routes work on Vercel.
