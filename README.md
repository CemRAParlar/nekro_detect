# nekro_detect
Minecraft için operatör bot tasarımı

import random

class NekroDetect:
    def __init__(self, name="NekroDetect"):
        self.name = name
        self.position = [0, 64, 0]  # Başlangıç pozisyonu [x, y, z]
        self.inventory = {"wood": 0, "stone": 0, "iron": 0}
        self.health = 100

    # 1. AI_Builder (İnşaat Görevleri)
    def ai_builder(self, structure, material, amount):
        if self.inventory.get(material, 0) >= amount:
            print(f"{self.name}, {structure} inşa ediyor: {amount} {material} kullanıldı.")
            self.inventory[material] -= amount
        else:
            print(f"{self.name}, yeterli {material} yok. İnşaat için {amount - self.inventory.get(material, 0)} daha gerekli.")

    # 2. AI_Conductor (Kaynak ve Ekipman Yönetimi)
    def ai_conductor(self, action, item, quantity):
        if action == "gather":
            self.inventory[item] = self.inventory.get(item, 0) + quantity
            print(f"{self.name}, {quantity} adet {item} topladı. Envanter: {self.inventory}")
        elif action == "use" and self.inventory.get(item, 0) >= quantity:
            self.inventory[item] -= quantity
            print(f"{self.name}, {quantity} adet {item} kullandı. Kalan: {self.inventory[item]}")
        else:
            print(f"{self.name}, yeterli {item} yok. {quantity - self.inventory.get(item, 0)} daha gerekli.")

    # 3. AI_Warrior (Savaş Görevleri)
    def ai_warrior(self, enemy_type, enemy_strength):
        damage_taken = random.randint(10, 30)
        self.health -= damage_taken
        attack_damage = enemy_strength * random.randint(2, 4)
        print(f"{self.name}, {enemy_type} ile savaştı ve {damage_taken} hasar aldı. Sağlık: {self.health}")
        print(f"{enemy_type} düşmana {attack_damage} hasar verildi.")
        if self.health <= 0:
            print(f"{self.name} yenildi! Bot sağlık kaybetti.")
            self.health = 0  # Sağlık sıfırlanır

    # Diğer Özellikler
    def update_position(self, x, y, z):
        self.position = [x, y, z]
        print(f"{self.name} yeni konumda: {self.position}")

    def gather_resources(self, resource_type, amount):
        if resource_type in self.inventory:
            self.inventory[resource_type] += amount
            print(f"{amount} adet {resource_type} toplandı. Envanter: {self.inventory}")
        else:
            print(f"{resource_type} bu bot tarafından toplanamaz.")

    def fight_enemy(self, enemy_strength):
        damage = random.randint(5, 20)
        self.health -= damage
        print(f"{self.name}, {enemy_strength} gücünde düşmanla savaştı. Sağlık: {self.health}")

    def mark_safe_zone(self):
        print(f"{self.name}, {self.position} konumunu güvenli bölge olarak işaretledi.")

    def heal(self, amount):
        self.health = min(100, self.health + amount)
        print(f"{self.name} {amount} sağlık puanı kazandı. Yeni sağlık: {self.health}")

    def plan_route(self):
        route = [random.randint(-10, 10) for _ in range(3)]
        self.position = [self.position[i] + route[i] for i in range(3)]
        print(f"{self.name} rotayı güncelledi: Yeni konum {self.position}")

    def check_tool(self, tool):
        has_tool = tool in ["balta", "kılıç", "kazma"]
        print(f"{self.name}, {tool} var mı? {'Evet' if has_tool else 'Hayır'}")
        return has_tool

    def nekromath_operation(self, a, b):
        result = a ** 2 + b ** 2
        print(f"{self.name} NekroMatematik sonucunu hesapladı: {result}")
        return result

    def generate_report(self):
        report = {
            "name": self.name,
            "position": self.position,
            "health": self.health,
            "inventory": self.inventory
        }
        print(f"{self.name} görev raporu: {report}")
        return report

# Botu çalıştırma örneği
bot = NekroDetect()

# AI_Builder ile inşaat görevi
bot.ai_builder("Ev", "wood", 15)

# AI_Conductor ile kaynak yönetimi
bot.ai_conductor("gather", "stone", 20)
bot.ai_conductor("use", "stone", 5)

# AI_Warrior ile savaş görevi
bot.ai_warrior("Zombi", 3)

# Diğer işlevler
bot.update_position(10, 65, -5)
bot.gather_resources("wood", 10)
bot.fight_enemy("Zombi")
bot.mark_safe_zone()
bot.heal(15)
bot.plan_route()
bot.check_tool("balta")
bot.nekromath_operation(3, 4)
bot.generate_report()

