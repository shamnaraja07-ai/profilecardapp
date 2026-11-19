# Test Report - Profile Card App

| | |
|---|---|
| **Project** | InternCircle Project 01 - Profile Card App (Flutter) |
| **Version** | 1.0.0 |
| **Test framework** | `flutter_test` (unit + widget tests) |
| **Test file** | `test/profile_card_test.dart` |
| **Report date** | 2026-11-19 |

## 1. Execution status (please read)

The tests were **written but not executed** when this report was prepared: the environment used to author the
project had no Flutter/Dart SDK available. Only a structural check (balanced brackets) of the Dart files was done.
**No pass/fail result in section 3 has been observed yet**, so all rows are marked *Not run*.

To produce real results (takes under a minute):

```bash
flutter pub get
flutter analyze
flutter test --reporter expanded 2>&1 | tee test_report.txt
```

Or push to GitHub: the workflow `.github/workflows/flutter-ci.yml` runs the same commands and uploads
`test_report.txt` and `coverage/lcov.info` as the **test-report** artifact (Actions tab -> latest run).
Then update the *Result* column below and paste the final summary line in section 4.

## 2. Scope

In scope: content shown on the card, the reusable `ContactRow`, the initials logic, and responsive layout
(centring, maximum width, narrow and short screens).
Out of scope: platform-specific behaviour, accessibility audits, golden (pixel) tests.

## 3. Automated test cases

| ID | Test | Requirement covered | Expected result | Result |
|---|---|---|---|---|
| UT-1 | `Profile.initials` uses first letters of first two words ("Meera Nair" -> `MN`, "  ada   b  c " -> `AB`) | Avatar with initials | Initials match | Not run |
| UT-2 | `Profile.initials` handles one word (`M`) and an empty name (`?`) | Avatar with initials (edge cases) | Initials match | Not run |
| WT-1 | Shows avatar initials, name and role | Avatar, name, role shown | `CircleAvatar` x1; texts `MN`, `Meera Nair`, `Flutter Intern` found | Not run |
| WT-2 | Shows exactly three contact rows with icons and text | Three contact rows | `ContactRow` x3; email, phone, location icons and texts found | Not run |
| WT-3 | `ContactRow` renders on its own | `ContactRow` is reusable | Icon and text found outside `ProfileCard` | Not run |
| WT-4 | App renders a custom `Profile` | Data-driven card | Custom initials, name and city shown | Not run |
| LT-1 | Wide screen (1200x800) | Centred, maximum width | Card width <= 360; horizontal centre at x = 600 | Not run |
| LT-2 | Narrow phone (320x568) | Works on narrow screens | No exception (no overflow); card edges inside 0..320 | Not run |
| LT-3 | Very short screen (320x300) | Works on small screens | No exception; content scrolls (`SingleChildScrollView` present) | Not run |

## 4. Result summary

Fill in after running: `__ passed, __ failed` (expected: 9 passed, 0 failed).

## 5. Manual checklist (from the project guide) - complete in DartPad

| Check | Pass? | Notes |
|---|---|---|
| The app runs without errors in DartPad | [ ] | |
| The card is centred and has a maximum width | [ ] | |
| Avatar, name, role and three contact rows are shown | [ ] | |
| `ContactRow` is a reusable widget | [ ] | |
| The screenshot shows a narrow phone layout | [ ] | |

## 6. Known limitations

- The tests use fictional sample data (`Meera Nair`, `example.com`); change `defaultProfile` and the matching
  expectations together if you personalise the card.
- Layout tests simulate screen sizes with `tester.view`; they confirm there is no overflow exception but do not
  compare rendered pixels.
