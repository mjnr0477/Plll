pulse-app/
 ├── App.js
 ├── package.json
 ├── assets/
 │    └── icon.png
 └── README.md{
  "name": "pulse-app",
  "version": "1.0.0",
  "main": "node_modules/expo/AppEntry.js",
  "scripts": {
    "start": "expo start",
    "android": "expo run:android",
    "ios": "expo run:ios",
    "web": "expo start --web"
  },
  "dependencies": {
    "expo": "~51.0.0",
    "expo-status-bar": "~1.12.0",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "react-native": "0.74.0",
    "react-native-web": "~0.19.0"
  },
  "private": true
}import React, { useState } from "react";
import { View, Text, TextInput, FlatList, TouchableOpacity, StyleSheet } from "react-native";
import { StatusBar } from "expo-status-bar";

export default function App() {
  const [message, setMessage] = useState("");
  const [pulseFeed, setPulseFeed] = useState([]);

  const sendMessage = () => {
    if (message.trim().length === 0) return;
    const newPulse = { id: Date.now().toString(), text: message.trim() };
    setPulseFeed([newPulse, ...pulseFeed]);
    setMessage("");
  };

  const renderPulse = ({ item }) => (
    <View style={styles.pulseItem}>
      <Text style={styles.pulseText}>{item.text}</Text>
    </View>
  );

  return (
    <View style={styles.container}>
      <Text style={styles.header}>💬 Pulse</Text>

      <FlatList
        data={pulseFeed}
        renderItem={renderPulse}
        keyExtractor={(item) => item.id}
        contentContainerStyle={{ flexGrow: 1 }}
        ListEmptyComponent={<Text style={styles.emptyText}>No pulses yet. Share what you feel ✨</Text>}
      />

      <View style={styles.inputRow}>
        <TextInput
          style={styles.input}
          placeholder="What's in your heart?"
          placeholderTextColor="#aaa"
          value={message}
          onChangeText={setMessage}
        />
        <TouchableOpacity style={styles.sendBtn} onPress={sendMessage}>
          <Text style={styles.sendText}>Send</Text>
        </TouchableOpacity>
      </View>

      <StatusBar style="light" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#0d0d0d",
    paddingTop: 60,
    paddingHorizontal: 15,
  },
  header: {
    fontSize: 28,
    color: "#fff",
    fontWeight: "bold",
    marginBottom: 15,
  },
  inputRow: {
    flexDirection: "row",
    alignItems: "center",
    backgroundColor: "#1c1c1c",
    borderRadius: 10,
    padding: 10,
    marginBottom: 10,
  },
  input: {
    flex: 1,
    color: "#fff",
    paddingHorizontal: 10,
  },
  sendBtn: {
    backgroundColor: "#007bff",
    paddingVertical: 8,
    paddingHorizontal: 16,
    borderRadius: 8,
  },
  sendText: {
    color: "#fff",
    fontWeight: "bold",
  },
  pulseItem: {
    backgroundColor: "#1f1f1f",
    padding: 12,
    borderRadius: 10,
    marginVertical: 5,
  },
  pulseText: {
    color: "#fff",
    fontSize: 16,
  },
  emptyText: {
    color: "#666",
    textAlign: "center",
    marginTop: 40,
    fontSize: 16,
  },
});# Plll
