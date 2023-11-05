<h1>HW1</h1>
    
```swift

import SwiftUI

struct ContentView: View {
    let displayFontType = [".default",".rounded",".monospaced",".serif"]
    
    @State var displayFontSelected = 0
    @State var isDeepScheme = false
    @State var colorArray: [Double] = [255.0, 255.0, 255.0]
    @State var stepperValue = 0
    @State var sliderValue = 0.0
    @State var date = Date()
    @State private var selectedLanguage = "English" // Default language
    
    var body: some View {
        NavigationView {
            Form {
                Section(header: Text("Font Settings")) {
                    Picker("Select Font", selection: $displayFontSelected) {
                        ForEach(0..<displayFontType.count, id: \.self) {
                            Text(self.displayFontType[$0])
                        }
                    }
                }
                
                Section(header: Text("Background Style")) {
                    Toggle("Dark Mode \(String(isDeepScheme))", isOn: $isDeepScheme)
                }
                
                Section(header: Text("Counter")) {
                    Stepper(value: $stepperValue) {
                        Text("Stepper \(stepperValue)")
                    }
                }
                
                Section(header: Text("Slider \(sliderValue, specifier: "%.2f")")) {
                    Slider(value: $sliderValue, in: 0...1)
                }
                
                Section(header: Text("Date")) {
                    DatePicker("date", selection: $date, displayedComponents: [.date])
                }
                
                Section(header: Text("Language")) {
                    Picker("Select Language", selection: $selectedLanguage) {
                        Text("English").tag("English")
                        Text("中文").tag("Chinese")
                    }
                    .onChange(of: selectedLanguage) { _ in
                        if selectedLanguage == "Chinese" {
                            // Change app's language to Chinese
                            // Update the app's language settings or reload the view to reflect the language change
                        } else {
                            // Change app's language to English
                            // Update the app's language settings or reload the view to reflect the language change
                        }
                    }
                }
            }
            .navigationTitle("Settings")
        }
    }
}

    
```
(https://youtube.com/shorts/eJEzWrw58KQ)
