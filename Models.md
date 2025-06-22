Simple Greeting Card Creator (MVP) 🎉

A SwiftUI application that allows users to create a simple, personalized digital greeting card. This project serves as a practical example of fundamental SwiftUI concepts, including state management, UI components, and basic app architecture.

🌟 Features

🖼️ Select Background Image: Choose from a predefined set of background images.

✍️ Custom Greeting Message: Input a personalized message for the card.

🎨 Full Style Control:

Change the text color from a list of options.

Select a custom font style.

Adjust the font size with a slider.

👀 Live Preview: See the card update in real-time as you make changes.

📸 Screenshot
<!-- TODO: Add a screenshot or a short GIF of the app in action here! -->


![alt text](https://via.placeholder.com/350x700/f0f0f0/000000?text=App+Screenshot+Goes+Here)

🛠️ Tech Stack & Core SwiftUI Concepts

SwiftUI Framework: The entire UI is built declaratively with SwiftUI.

MVVM-like Architecture: The app uses a ViewModel (CardViewModel) to separate UI state and logic from the View.

@StateObject & @ObservedObject: To create and manage the lifecycle of the CardViewModel as the "Source of Truth".

@Published: To automatically notify the UI of any state changes within the ViewModel.

UI Components: ZStack, VStack, Form, Section, Image, Text, TextField, Picker, Slider.

Data-Driven Views: ForEach is used to dynamically generate lists of options from data models.

Identifiable & Hashable: Protocols used on data models to ensure seamless integration with SwiftUI components like Picker and ForEach.

📂 Project Structure

The project code is organized to separate concerns, making it clean and easy to navigate.

CardCreatorView.swift: Contains the main SwiftUI View for the user interface.

Models.swift: Defines all data structures (structs) and the ViewModel (class) for the application.

Assets.xcassets: Stores all image assets (like background images) and can also define custom color sets.

🏗️ Data Models & Architecture

The application's architecture is centered around a CardViewModel which acts as the single source of truth for the UI.

CardViewModel

This ObservableObject class holds the current state of the greeting card being edited. The View subscribes to this object and updates automatically when its @Published properties change.

Property	Type	Description
greetingText	String	Stores the user's custom message that appears on the card.
selectedFontSize	CGFloat	The current size of the font for the greeting text.
selectedBackground	BackgroundOption	The currently selected BackgroundOption object.
selectedFont	FontOption	The currently selected FontOption object.
selectedColor	Color	The currently selected Color for the greeting text.
Core Data Structures

These structs define the individual, selectable items. They conform to Identifiable and Hashable to work seamlessly with SwiftUI.

BackgroundOption

Represents a single background image choice.

Property	Type	Description
id	UUID	A unique identifier for the instance.
imageName	String	The name of the image in the Assets.xcassets catalog.
FontOption

Represents a single font style choice.

Property	Type	Description
id	UUID	A unique identifier for the instance.
fontName	String	The system name for the font (e.g., "AvenirNext-Bold").
displayName	String	A user-friendly name for display in the UI (e.g., "Avenir Bold").
AppData (Static Data Provider)

This struct acts as a centralized, static container for all available options, making it easy to manage data in one place.

Property	Type	Description
backgroundOptions	[BackgroundOption]	A static array of all available BackgroundOptions.
fontOptions	[FontOption]	A static array of all available FontOptions.
colorOptions	[Color]	A static array of all available Colors for the text.
🚀 Getting Started

Clone the repository.

Generated bash
git clone [your-repository-url]


Add Assets: Place your background images (e.g., bg_beach.jpg, bg_forest.jpg) into the Assets.xcassets catalog. Ensure the names match those defined in AppData within the Models.swift file.

Open in Xcode: Open the .xcodeproj file.

Build and Run: Select an iOS simulator or a physical device and press the Run button (▶).

🔮 Future Enhancements

Save & Share: Implement functionality to save the created card to the photo library and share it via the system share sheet.

More Content: Allow users to add images from their own photo library or add "stickers" on top of the card.

Templates: Create pre-defined card templates for different occasions (Birthday, Thank You, etc.).

Animations: Add subtle animations to make the user experience more delightful.

📝 License

This project is licensed under the MIT License.
