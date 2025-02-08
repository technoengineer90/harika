# Aylık gelir gider ve alışveriş listesi
class BudgetTracker:
    def __init__(self, monthly_income):
        self.monthly_income = monthly_income
        self.expenses = []
        self.shopping_list = []
    
    def add_expense(self, name, amount):
        self.expenses.append((name, amount))
    
    def add_to_shopping_list(self, item, price):
        self.shopping_list.append((item, price))
    
    def total_expenses(self):
        return sum(amount for _, amount in self.expenses)
    
    def total_shopping_cost(self):
        return sum(price for _, price in self.shopping_list)
    
    def remaining_budget(self):
        return self.monthly_income - self.total_expenses() - self.total_shopping_cost()
    
    def budget_status(self):
        remaining = self.remaining_budget()
        if remaining < 0:
            return f"Bütçeniz {abs(remaining)} TL aşıldı! Harcamalarınızı gözden geçirin."
        else:
            return f"Kalan bütçeniz: {remaining} TL"
    
    def show_summary(self):
        print("Giderler:")
        for name, amount in self.expenses:
            print(f"- {name}: {amount} TL")
        print("\nAlışveriş Listesi:")
        for item, price in self.shopping_list:
            print(f"- {item}: {price} TL")
        print("\nToplam giderler:", self.total_expenses(), "TL")
        print("Toplam alışveriş harcaması:", self.total_shopping_cost(), "TL")
        print(self.budget_status())

# PyCharm'da çalıştırmak için
if __name__ == "__main__":
    monthly_income = float(input("Aylık geliriniz: "))
    budget = BudgetTracker(monthly_income)
    
    while True:
        print("\n1. Gider ekle")
        print("2. Alışveriş listesine ekle")
        print("3. Özeti göster")
        print("4. Çıkış")
        choice = input("Seçiminiz: ")
        
        if choice == "1":
            name = input("Gider adı: ")
            amount = float(input("Tutar: "))
            budget.add_expense(name, amount)
        elif choice == "2":
            item = input("Ürün adı: ")
            price = float(input("Fiyat: "))
            budget.add_to_shopping_list(item, price)
        elif choice == "3":
            budget.show_summary()
        elif choice == "4":
            print("Çıkış yapılıyor...")
            break
        else:
            print("Geçersiz seçim, tekrar deneyin.")
