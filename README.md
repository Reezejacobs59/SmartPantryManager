# Smart Pantry Manager

A native **Java Android** app that helps reduce food waste. You record the ingredients you
actually have at home (your "pantry"), and the app suggests recipes you can cook **using strictly
those ingredients** - no shopping trip required.

Built for *Mobile App Development 700 - Practical Assignment* (Richfield Graduate Institute of Technology).

## Features
- **Pantry management (full CRUD):** add, view, edit and delete ingredients (name, quantity, unit, optional expiry date).
- **15 pre-loaded Indian recipes** (seeded into the database on first run), each with its own colour:
  Dal Tadka, Aloo Gobi, Chana Masala, Palak Paneer, Paneer Butter Masala, Jeera Rice, Vegetable Pulao,
  Masoor Dal, Egg Curry, Chicken Curry, Baingan Bharta, Rajma, Bhindi Masala, Aloo Paratha, Masala Chai.
- **Strict matching rule:** a recipe is suggested only if *every* ingredient is in the pantry in at least the
  required quantity. 4 of 5 ingredients = **not** suggested.
- **Robust matching:** ignores capital letters and singular/plural ("Tomatoes" = "tomato"), understands common
  synonyms (curd = yogurt, brinjal = eggplant ...) and converts units (kg/g, l/ml, tsp/tbsp/cup).
- **Friendly empty state:** "No recipes match your pantry yet - add more ingredients".
- **Optional "Almost There" list** (recipes missing exactly one ingredient) - clearly separated; switch on in Settings.
- **Expiring-soon alerts** (Settings toggle), input validation on the form, bottom navigation bar.
- **No Google Maps, no GPS/location, no permissions.**

## Screens
1. Pantry List (`MainActivity`)  2. Add/Edit Ingredient (`AddEditIngredientActivity`)
3. Suggested Recipes (`SuggestedRecipesActivity`)  4. Recipe Detail (`RecipeDetailActivity`)  5. Settings (`SettingsActivity`)

## Database choice: SQLite (`SQLiteOpenHelper`)
SQLite is built into Android, works fully offline, needs no account/server/permissions, and suits small personal
data. It supports relational tables and foreign keys, which fit the recipe -> ingredients structure.
Tables: `pantry_items`, `recipes`, `recipe_ingredients`. Data is stored on the device, so it persists after the app is closed.

## Project structure
```
app/src/main/java/com/example/smartpantry/
  model/    PantryItem, Recipe, RecipeIngredient
  db/       DatabaseHelper (CRUD), RecipeSeeder (15 recipes)
  logic/    RecipeMatcher (strict rule), IngredientNormalizer, UnitConverter   <- pure Java, unit tested
  adapter/  PantryAdapter, RecipeAdapter (RecyclerView)
  util/     NavHelper, Prefs, ExpiryHelper, ColorUtil
  *.java    the five Activities
app/src/test/  RecipeMatcherTest (JUnit)
```

## Setup / run instructions
**Requirements:** Android Studio (Hedgehog / Iguana or newer), JDK 17 (bundled with Android Studio), internet for the first Gradle sync.

1. Clone the repo: `git clone https://github.com/<your-username>/SmartPantryManager.git`
2. In Android Studio choose **File > Open** and select the `SmartPantryManager` folder.
3. Wait for **Gradle sync** to finish (first time downloads dependencies).
4. Create/select a device: **Tools > Device Manager** (e.g. Pixel 6, API 34) or plug in a phone with USB debugging.
5. Press the green **Run** button.
6. Tip: open **Settings > Load sample pantry** to quickly add ingredients, then open the **Recipes** tab.

**Run the unit tests:** right-click `app/src/test/.../RecipeMatcherTest` > *Run*.

## Author
[Your Name] - [Student number] - Mobile App Development 700
