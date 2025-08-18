import 'package:flutter/material.dart';

void main() {
  runApp(const InstaReplyAI());
}

class InstaReplyAI extends StatelessWidget {
  const InstaReplyAI({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Insta Reply AI',
      theme: ThemeData(
        primarySwatch: Colors.deepPurple,
      ),
      home: const ReplyPage(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class ReplyPage extends StatefulWidget {
  const ReplyPage({super.key});

  @override
  State<ReplyPage> createState() => _ReplyPageState();
}

class _ReplyPageState extends State<ReplyPage> {
  final TextEditingController _controller = TextEditingController();
  String _reply = "";
  String _tone = "casual";

  void _generateReply() {
    String message = _controller.text.trim();
    if (message.isEmpty) {
      setState(() {
        _reply = "Please enter a message first.";
      });
      return;
    }

    String reply;
    switch (_tone) {
      case "casual":
        reply = "Haha I get you! ${message.split(" ").take(5).join(" ")}... that's interesting!";
        break;
      case "flirty":
        reply = "Oh really? 😉 ${message.split(" ").take(4).join(" ")}... you just made me smile.";
        break;
      case "funny":
        reply = "😂 lol, ${message.split(" ").take(4).join(" ")}... you're too much!";
        break;
      case "deep":
        reply = "I hear you. ${message.split(" ").take(6).join(" ")}... it really makes me think.";
        break;
      default:
        reply = "That's interesting!";
    }

    setState(() {
      _reply = reply;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Insta Reply AI"),
        centerTitle: true,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              decoration: const InputDecoration(
                border: OutlineInputBorder(),
                hintText: "Paste the Instagram message here...",
              ),
              maxLines: 3,
            ),
            const SizedBox(height: 12),
            DropdownButton<String>(
              value: _tone,
              onChanged: (value) {
                setState(() {
                  _tone = value!;
                });
              },
              items: const [
                DropdownMenuItem(value: "casual", child: Text("Casual/Friendly 👋")),
                DropdownMenuItem(value: "flirty", child: Text("Flirty/Romantic 💕")),
                DropdownMenuItem(value: "funny", child: Text("Playful/Funny 🎉")),
                DropdownMenuItem(value: "deep", child: Text("Deep/Supportive 🌙")),
              ],
            ),
            const SizedBox(height: 12),
            ElevatedButton(
              onPressed: _generateReply,
              child: const Text("Generate Reply"),
            ),
            const SizedBox(height: 20),
            Text(
              _reply,
              style: const TextStyle(fontSize: 16, fontWeight: FontWeight.w500),
            ),
          ],
        ),
      ),
    );
  }
}# lib-main.dart
