# flutter_theming_system

A new Flutter project.

## Getting Started


While primarySwatch is convenient, using a ColorScheme is a more flexible and powerful approach.

theme: ThemeData(
  colorScheme: ColorScheme.fromSeed(
    seedColor: Colors.deepPurple, // Auto-generates a palette
  ),
  useMaterial3: true, // Switches to Material 3 design if needed
),

ColorScheme introduces more control over different color aspects, like secondary, background, and error colors:
theme: ThemeData(
  colorScheme: ColorScheme(
    primary: Colors.deepPurple,
    secondary: Colors.amber,
    background: Colors.white,
    surface: Colors.grey[200]!,
    error: Colors.red,
    onPrimary: Colors.white,
    onSecondary: Colors.black,
    onError: Colors.white,
    onBackground: Colors.black,
    onSurface: Colors.black,
    brightness: Brightness.light,
  ),
),
Defining Custom Text Styles
theme: ThemeData(
  textTheme: TextTheme(
    headline1: TextStyle(fontSize: 32.0, fontWeight: FontWeight.bold),
    bodyText1: TextStyle(fontSize: 16.0),
    caption: TextStyle(fontSize: 12.0, color: Colors.grey),
  ),
),

Text(
  'Welcome to Flutter',
  style: Theme.of(context).textTheme.headline1,
)

Step 4: Dark Theme Implementation
MaterialApp(
  theme: ThemeData.light(),
  darkTheme: ThemeData.dark(),
  themeMode: ThemeMode.system, // Automatically switches based on system settings
),
If you want to customize your dark theme:
darkTheme: ThemeData(
  colorScheme: ColorScheme.dark(
    primary: Colors.blueGrey,
    secondary: Colors.cyan,
  ),
),

Step 6: Custom Theme Extension
To take theming to a pro level, you might want to define your own custom theme properties (e.g., for padding, borders, or custom colors). Flutter allows you to extend the theme system by adding custom extensions.

Define the Custom Theme:
class MyCustomTheme extends ThemeExtension<MyCustomTheme> {
  final Color customColor;

  MyCustomTheme({required this.customColor});

  @override
  MyCustomTheme copyWith({Color? customColor}) {
    return MyCustomTheme(
      customColor: customColor ?? this.customColor,
    );
  }

  @override
  MyCustomTheme lerp(ThemeExtension<MyCustomTheme>? other, double t) {
    if (other is! MyCustomTheme) return this;
    return MyCustomTheme(
      customColor: Color.lerp(customColor, other.customColor, t)!,
    );
  }
}
Include the Custom Theme in Your App:
theme: ThemeData(
  extensions: [
    MyCustomTheme(customColor: Colors.orange),
  ],
),
Use the Custom Theme:
final customTheme = Theme.of(context).extension<MyCustomTheme>();

Container(
  color: customTheme?.customColor,
  child: Text('Custom Theme Color!'),
)


: Using Google Fonts and Custom Fonts
import 'package:google_fonts/google_fonts.dart';

theme: ThemeData(
  textTheme: GoogleFonts.robotoTextTheme(
    Theme.of(context).textTheme,
  ),
),
You can also use custom fonts by adding them to your pubspec.yaml file:
flutter:
  fonts:
    - family: CustomFont
      fonts:
        - asset: fonts/CustomFont-Regular.ttf
        - asset: fonts/CustomFont-Bold.ttf
          weight: 700
Step 8: Global vs Local Themes
For modularity, you can apply themes at the widget level using Theme widget to override the global theme for specific sections:

Theme(
  data: Theme.of(context).copyWith(
    colorScheme: ColorScheme.light(
      primary: Colors.green,
    ),
  ),
  child: ElevatedButton(
    onPressed: () {},
    child: Text('Locally Themed Button'),
  ),
)



Here’s a detailed breakdown of the most important ColorScheme properties in Flutter and when to use each of them in your app. This will help you maintain a structured and consistent color palette:

1. primary
Purpose: This is the most prominent color of your application, representing the brand or the theme of your app.
When to use: Use this color for key UI elements like the app bar, buttons, progress indicators, and active selections. It defines the visual identity of your app.
Example: AppBar, ElevatedButton, FloatingActionButton.
2. onPrimary
Purpose: This color is used on top of the primary color.
When to use: Use onPrimary for elements like text, icons, or borders that appear on top of the primary color. For instance, white text on a blue button.
Example: Text inside a button (ElevatedButton) or AppBar title.
3. secondary
Purpose: A less dominant, complementary color often used for accentuating UI elements.
When to use: Use secondary for secondary actions or elements that support the primary color, such as toggle buttons, selection controls (like sliders, checkboxes), or floating chips.
Example: Action buttons in dialogs, filter chips, toggle buttons.
4. onSecondary
Purpose: Color used for text, icons, or other elements that are placed on top of the secondary color.
When to use: Use onSecondary to ensure readability and contrast when placing elements over the secondary color.
Example: Text or icons inside a secondary-colored toggle button.
5. error
Purpose: The color used to indicate errors, warnings, or anything that requires attention.
When to use: Use error color for things like form validation errors, failure dialogs, error icons, or any other alert-based element.
Example: TextField error messages, error banners, or red icons in a failed state.
6. onError
Purpose: The color used for elements placed on top of the error color.
When to use: Use onError for text or icons that need to be visible on a red (error) background. Typically, this is white for contrast on red.
Example: Text inside an error dialog or button labels on an alert box.
7. background
Purpose: The main background color of your app.
When to use: Use background for large areas of your app like screens, pages, and the main container where all UI elements are placed. It's the canvas for your UI.
Example: Scaffold background, Drawer, large containers that serve as the backdrop for UI elements.
8. onBackground
Purpose: The color used for elements placed on top of the background color.
When to use: Use onBackground for text, icons, or interactive elements that appear on the background. This is often the primary text color or icon color.
Example: Main body text on a screen, icons or buttons that are placed directly on the background.
9. surface
Purpose: The background color for components like cards, sheets, and dialogs.
When to use: Use surface for smaller, elevated containers such as cards or dialogs. It usually contrasts a little with the background color to stand out but not overwhelm.
Example: Material Card, Dialog background, Bottom Sheets, Tooltips.
10. onSurface
Purpose: The color used for elements placed on top of a surface.
When to use: Use onSurface for text, icons, or other content that sits on top of a surface element, such as text inside a card or a dialog.
Example: Text in a card, icon colors on a dialog, or button text in a bottom sheet.
Putting It All Together
When creating your app’s theme, these ColorScheme properties should work together to ensure a consistent, accessible, and user-friendly UI. Here's a high-level example of how you might apply these properties in a real-world context:

Buttons:
primary for the button background.
onPrimary for the text on the button.
Error dialogs:
error for the background of the alert.
onError for the text on the error alert.
Cards:
surface for the card background.
onSurface for text and icons inside the card.
Main Background:
background for the screen's default background color.
onBackground for the text that appears directly on the background.
The combination of these properties ensures that every part of your app, from the most prominent elements to the smallest details, has a consistent look and feel with clear visual hierarchy.


1. canvasColor
Purpose: This is the overall background color of your app window or screen.
When to use: Use canvasColor for large background areas such as the entire app window, behind drawers, and large containers. It usually serves as the very base layer of the UI, on which other elements are drawn.
Example: The area behind the Scaffold, Drawer background, or screens without a Scaffold.
dart
Copy code
theme: ThemeData(
  canvasColor: Colors.grey[100], // Light grey background for the entire app window
),
2. scaffoldBackgroundColor
Purpose: This specifically controls the background color of the Scaffold widget, which is one of the most commonly used layout components in Flutter.
When to use: Use scaffoldBackgroundColor to set the background color of your app’s main screens. It covers areas like the app bar background, body area, and navigation bar background.
Example: For setting the main screen’s background color.
dart
Copy code
theme: ThemeData(
  scaffoldBackgroundColor: Colors.white, // White background for main screens
),
3. highlightColor
Purpose: This color appears when a widget is tapped and held down (e.g., when the user long presses a button or other interactive widget).
When to use: Use highlightColor to give visual feedback when a user interacts with elements like buttons or list items. This color is usually a lighter shade of the widget’s color or a ripple effect.
Example: When a button or card is tapped or long pressed.
dart
Copy code
theme: ThemeData(
  highlightColor: Colors.blue.withOpacity(0.3), // Light blue color on touch
),
4. focusColor
Purpose: Defines the color for elements that are currently focused (i.e., they will receive keyboard or other input). This is particularly useful for forms, dialogs, or navigational elements.
When to use: Use focusColor to visually highlight which widget currently has focus, especially in apps with input fields, keyboard navigation, or accessibility features.
Example: When a text field, button, or form element receives focus.
dart
Copy code
theme: ThemeData(
  focusColor: Colors.blueAccent, // Blue accent to indicate focus
),
5. hoverColor
Purpose: The color shown when a user hovers over an interactive widget with a pointer device (like a mouse or stylus). This is primarily useful for desktop and web applications.
When to use: Use hoverColor for elements that need to react to mouse hover events, like buttons or clickable icons. It's particularly useful in web or desktop versions of your Flutter app.
Example: When hovering over a button on a desktop app.
dart
Copy code
theme: ThemeData(
  hoverColor: Colors.blue.withOpacity(0.1), // Light blue hover effect
),
6. splashColor
Purpose: Defines the ripple effect color when a widget like a button is tapped.
When to use: Use splashColor to control the color of the ripple animation that spreads when users tap buttons, icons, or list items. It provides immediate feedback to the user that their tap has been registered.
Example: A ripple animation when a button is tapped.
dart
Copy code
theme: ThemeData(
  splashColor: Colors.blue.withOpacity(0.2), // Subtle ripple effect color
),
7. cardColor
Purpose: Sets the background color for Card widgets, which are used to display related information in a rectangular, elevated container.
When to use: Use cardColor for controlling the background color of your cards, which helps cards stand out from the rest of the content.
Example: Set a custom color for Card widgets in a list.
dart
Copy code
theme: ThemeData(
  cardColor: Colors.white, // Default white card color
),
8. dividerColor
Purpose: Controls the color of Divider and PopupMenuDivider widgets, which are thin lines used to separate content in lists, menus, or between sections.
When to use: Use dividerColor when you want to customize the color of dividers in lists, menus, or other UI elements where sections need to be separated.
Example: Dividing list items with a custom color.
dart
Copy code
theme: ThemeData(
  dividerColor: Colors.grey[300], // Light grey dividers
),
9. dialogBackgroundColor
Purpose: Controls the background color of dialogs, which are typically modal popups used to show important information or get user input.
When to use: Use dialogBackgroundColor to customize the appearance of dialogs (like alerts, form dialogs, or confirmation dialogs) by setting a background color that fits your theme.
Example: Custom dialog background.
dart
Copy code
theme: ThemeData(
  dialogBackgroundColor: Colors.white, // White background for dialogs
),
10. bottomAppBarColor
Purpose: Sets the background color for the bottom app bar, often used with BottomNavigationBar or FloatingActionButton.
When to use: Use bottomAppBarColor to customize the background color of the bottom app bar, especially when you want it to match the overall theme of your app.
Example: For the background of the bottom navigation area.
dart
Copy code
theme: ThemeData(
  bottomAppBarColor: Colors.grey[900], // Dark background for bottom app bar
),
11. disabledColor
Purpose: Controls the color for disabled UI elements, such as buttons or text fields that are not interactive.
When to use: Use disabledColor to visually indicate that a widget is inactive and not usable. Typically, this is a muted or gray color that contrasts with active elements.
Example: Disabled buttons, text fields, or icons.
dart
Copy code
theme: ThemeData(
  disabledColor: Colors.grey[400], // Light grey for disabled elements
),
12. errorColor
Purpose: Similar to ColorScheme.error, this is the color used for error states throughout the app.
When to use: Use errorColor for any UI elements that need to display error states or warnings, such as form validation error messages, failed actions, or warnings.
Example: Red color for error text or icons.
dart
Copy code
theme: ThemeData(
  errorColor: Colors.red, // Standard red for error states
),
13. appBarTheme
Purpose: Allows you to define a custom theme specifically for the AppBar widget.
When to use: Use appBarTheme to customize the look of all AppBars in your app, including their background color, text styles, and elevation.
Example: Customizing the AppBar across the app.
dart
Copy code
theme: ThemeData(
  appBarTheme: AppBarTheme(
    color: Colors.blue, // AppBar background color
    titleTextStyle: TextStyle(color: Colors.white, fontSize: 20),
  ),
),
Conclusion
By understanding and utilizing these ThemeData properties, you can create a consistent, polished, and professional-looking UI. These properties allow you to customize the look and feel of almost every element in your app, ensuring everything from backgrounds to interactions feels cohesive and user-friendly.



