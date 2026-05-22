import { useState, useEffect, useRef } from "react";

const CATEGORIES = [
  { id: "food", label: "Food & Dining", icon: "🍜", color: "#FF6B6B" },
  { id: "transport", label: "Transport", icon: "🚗", color: "#4ECDC4" },
  { id: "shopping", label: "Shopping", icon: "🛍️", color: "#FFE66D" },
  { id: "health", label: "Health", icon: "💊", color: "#A8E6CF" },
  { id: "entertainment", label: "Entertainment", icon: "🎬", color: "#C3A6FF" },
  { id: "bills", label: "Bills & Utilities", icon: "💡", color: "#FFB347" },
  { id: "savings", label: "Savings", icon: "🏦", color: "#74B9FF" },
  { id: "other", label: "Other", icon: "📦", color: "#CCCCCC" },
];

const MONTHS = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];

function generateId() {
  return Math.random().toString(36).substr(2, 9);
}

function formatCurrency(amount) {
  return new Intl.NumberFormat("en-US", { style: "currency", currency: "USD", minimumFractionDigits: 2 }).format(amount);
}

function getMonthKey(date) {
  const d = new Date(date);
  return `${d.getFullYear()}-${d.getMonth()}`;
}

export default function FinanceApp() {
  const [view, setView] = useState("dashboard");
  const [transactions, setTransactions] = useState([
    { id: generateId(), type: "expense", category: "food", amount: 24.5, note: "Lunch at noodle bar", date: new Date().toISOString() },
    { id: generateId(), type: "expense", category: "transport", amount: 12, note: "Uber ride", date: new Date(Date.now() - 86400000).toISOString() },
    { id: generateId(), type: "income", category: "other", amount: 3200, note: "Monthly salary", date: new Date(Date.now() - 2 * 86400000).toISOString() },
    { id: generateId(), type: "expense", category: "bills", amount: 89, note: "Electric bill", date: new Date(Date.now() - 3 * 86400000).toISOString() },
    { id: generateId(), type: "savings", category: "savings", amount: 500, note: "Emergency fund", date: new Date(Date.now() - 4 * 86400000).toISOString() },
    { id: generateId(), type: "expense", category: "shopping", amount: 67.3, note: "Groceries", date: new Date(Date.now() - 5 * 86400000).toISOString() },
    { id: generateId(), type: "expense", category: "entertainment", amount: 15.99, note: "Netflix", date: new Date(Date.now() - 6 * 86400000).toISOString() },
  ]);
  const [savingsGoals, setSavingsGoals] = useState([
    { id: generateId(), name: "Vacation Fund", target: 2000, current: 650, icon: "✈️", color: "#FF6B6B" },
    { id: generateId(), name: "New Laptop", target: 1500, current: 900, icon: "💻", color: "#4ECDC4" },
    { id: generateId(), name: "Emergency Fund", target: 5000, current: 1200, icon: "🛡️", color: "#FFE66D" },
  ]);
  const [budget, setBudget] = useState({ food: 400, transport: 150, shopping: 300, health: 100, entertainment: 100, bills: 200 });
  const [addModal, setAddModal] = useState(false);
  const [goalModal, setGoalModal] = useState(false);
  const [form, setForm] = useState({ type: "expense", category: "food", amount: "", note: "", date: new Date().toISOString().split("T")[0] });
  const [goalForm, setGoalForm] = useState({ name: "", target: "", icon: "⭐", color: "#FF6B6B" });
  const [animateIn, setAnimateIn] = useState(false);

  useEffect(() => {
    setTimeout(() => setAnimateIn(true), 50);
  }, []);

  const thisMonthTx = transactions.filter(t => getMonthKey(t.date) === getMonthKey(new Date()));
  const totalIncome = thisMonthTx.filter(t => t.type === "income").reduce((s, t) => s + t.amount, 0);
  const totalExpenses = thisMonthTx.filter(t => t.type === "expense").reduce((s, t) => s + t.amount, 0);
  const totalSavings = thisMonthTx.filter(t => t.type === "savings").reduce((s, t) => s + t.amount, 0);
  const balance = totalIncome - totalExpenses - totalSavings;

  const expenseByCategory = CATEGORIES.reduce((acc, cat) => {
    acc[cat.id] = thisMonthTx.filter(t => t.type === "expense" && t.category === cat.id).reduce((s, t) => s + t.amount, 0);
    return acc;
  }, {});

  function addTransaction() {
    if (!form.amount || isNaN(parseFloat(form.amount))) return;
    const tx = { id: generateId(), ...form, amount: parseFloat(form.amount), date: new Date(form.date).toISOString() };
    setTransactions(prev => [tx, ...prev]);
    setAddModal(false);
    setForm({ type: "expense", category: "food", amount: "", note: "", date: new Date().toISOString().split("T")[0] });
  }

  function addGoal() {
    if (!goalForm.name || !goalForm.target) return;
    setSavingsGoals(prev => [...prev, { id: generateId(), ...goalForm, target: parseFloat(goalForm.target), current: 0 }]);
    setGoalModal(false);
    setGoalForm({ name: "", target: "", icon: "⭐", color: "#FF6B6B" });
  }

  function deleteTransaction(id) {
    setTransactions(prev => prev.filter(t => t.id !== id));
  }

  function getCat(id) {
    return CATEGORIES.find(c => c.id === id) || CATEGORIES[7];
  }

  const recentTx = [...transactions].sort((a, b) => new Date(b.date) - new Date(a.date)).slice(0, 8);

  return (
    <div style={{
      minHeight: "100vh",
      background: "#0D0D0D",
      color: "#F0EDE8",
      fontFamily: "'DM Sans', 'Helvetica Neue', sans-serif",
      display: "flex",
      flexDirection: "column",
    }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600;700&family=Syne:wght@700;800&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; }
        ::-webkit-scrollbar { width: 4px; } ::-webkit-scrollbar-track { background: #1a1a1a; } ::-webkit-scrollbar-thumb { background: #333; border-radius: 2px; }
        .card { background: #161616; border: 1px solid #2a2a2a; border-radius: 20px; transition: all 0.2s ease; }
        .card:hover { border-color: #3a3a3a; }
        .btn { cursor: pointer; border: none; border-radius: 12px; font-family: 'DM Sans', sans-serif; font-weight: 600; transition: all 0.15s ease; }
        .btn:hover { transform: translateY(-1px); }
        .btn:active { transform: translateY(0); }
        .nav-btn { background: none; border: none; cursor: pointer; font-family: 'DM Sans', sans-serif; }
        .slide-in { animation: slideUp 0.4s ease forwards; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .tag { display: inline-flex; align-items: center; gap: 6px; padding: 4px 10px; border-radius: 20px; font-size: 12px; font-weight: 600; }
        .modal-bg { position: fixed; inset: 0; background: rgba(0,0,0,0.8); backdrop-filter: blur(6px); z-index: 100; display: flex; align-items: center; justify-content: center; }
        .modal { background: #161616; border: 1px solid #2a2a2a; border-radius: 24px; padding: 28px; width: 90%; max-width: 420px; }
        .input { background: #0D0D0D; border: 1px solid #2a2a2a; border-radius: 12px; color: #F0EDE8; padding: 12px 16px; font-family: 'DM Sans', sans-serif; font-size: 15px; width: 100%; outline: none; transition: border-color 0.2s; }
        .input:focus { border-color: #FF6B6B; }
        .progress-bar { height: 6px; background: #222; border-radius: 3px; overflow: hidden; }
        .progress-fill { height: 100%; border-radius: 3px; transition: width 0.6s ease; }
        .tab { padding: 8px 18px; border-radius: 10px; font-size: 14px; font-weight: 500; color: #666; transition: all 0.2s; }
        .tab.active { background: #FF6B6B; color: white; }
        select option { background: #161616; }
      `}</style>

      {/* Header */}
      <div style={{ padding: "20px 20px 0", display: "flex", justifyContent: "space-between", alignItems: "center" }}>
        <div>
          <div style={{ fontFamily: "'Syne', sans-serif", fontSize: 22, fontWeight: 800, letterSpacing: -0.5 }}>
            SPNDX
          </div>
          <div style={{ color: "#555", fontSize: 12, marginTop: 2 }}>Daily Finance Manager</div>
        </div>
        <button className="btn" onClick={() => setAddModal(true)}
          style={{ background: "#FF6B6B", color: "white", padding: "10px 18px", fontSize: 13, display: "flex", alignItems: "center", gap: 8 }}>
          + Add
        </button>
      </div>

      {/* Balance Card */}
      <div style={{ padding: "20px 20px 0" }} className={animateIn ? "slide-in" : ""}>
        <div className="card" style={{
          padding: 24,
          background: "linear-gradient(135deg, #1a1a1a 0%, #0f0f0f 100%)",
          position: "relative", overflow: "hidden"
        }}>
          <div style={{ position: "absolute", top: -40, right: -40, width: 180, height: 180, background: "radial-gradient(circle, rgba(255,107,107,0.12) 0%, transparent 70%)", borderRadius: "50%" }} />
          <div style={{ color: "#666", fontSize: 13, marginBottom: 4 }}>Available Balance</div>
          <div style={{ fontFamily: "'Syne', sans-serif", fontSize: 42, fontWeight: 800, color: balance >= 0 ? "#F0EDE8" : "#FF6B6B" }}>
            {formatCurrency(balance)}
          </div>
          <div style={{ display: "flex", gap: 20, marginTop: 20 }}>
            {[
              { label: "Income", value: totalIncome, color: "#4ECDC4", icon: "↑" },
              { label: "Expenses", value: totalExpenses, color: "#FF6B6B", icon: "↓" },
              { label: "Savings", value: totalSavings, color: "#74B9FF", icon: "🏦" },
            ].map(item => (
              <div key={item.label}>
                <div style={{ color: "#555", fontSize: 11 }}>{item.label}</div>
                <div style={{ color: item.color, fontWeight: 700, fontSize: 16, marginTop: 2 }}>
                  <span style={{ marginRight: 3 }}>{item.icon}</span>{formatCurrency(item.value)}
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Nav */}
      <div style={{ display: "flex", gap: 8, padding: "16px 20px 8px", overflowX: "auto" }}>
        {[["dashboard","📊 Dashboard"],["transactions","📋 History"],["savings","🏦 Savings"],["budget","📌 Budget"]].map(([key, label]) => (
          <button key={key} className={`tab ${view === key ? "active" : ""}`} onClick={() => setView(key)}
            style={{ whiteSpace: "nowrap", background: view === key ? "#FF6B6B" : "#161616", border: "1px solid #2a2a2a", cursor: "pointer", borderRadius: 10 }}>
            {label}
          </button>
        ))}
      </div>

      {/* Content */}
      <div style={{ padding: "8px 20px 100px", flex: 1, overflowY: "auto" }}>

        {/* DASHBOARD */}
        {view === "dashboard" && (
          <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
            {/* Spending by Category */}
            <div className="card" style={{ padding: 20 }}>
              <div style={{ fontWeight: 700, marginBottom: 16, fontSize: 15 }}>This Month's Spending</div>
              {CATEGORIES.filter(c => c.id !== "savings" && expenseByCategory[c.id] > 0).sort((a, b) => expenseByCategory[b.id] - expenseByCategory[a.id]).map(cat => {
                const spent = expenseByCategory[cat.id];
                const budgetAmt = budget[cat.id] || 0;
                const pct = budgetAmt > 0 ? Math.min((spent / budgetAmt) * 100, 100) : 0;
                return (
                  <div key={cat.id} style={{ marginBottom: 14 }}>
                    <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 6 }}>
                      <span style={{ fontSize: 13 }}>{cat.icon} {cat.label}</span>
                      <span style={{ fontSize: 13, fontWeight: 600, color: cat.color }}>{formatCurrency(spent)}</span>
                    </div>
                    {budgetAmt > 0 && (
                      <div className="progress-bar">
                        <div className="progress-fill" style={{ width: `${pct}%`, background: pct > 85 ? "#FF6B6B" : cat.color }} />
                      </div>
                    )}
                  </div>
                );
              })}
              {Object.values(expenseByCategory).every(v => v === 0) && (
                <div style={{ color: "#555", fontSize: 14, textAlign: "center", padding: "20px 0" }}>No expenses this month yet</div>
              )}
            </div>

            {/* Recent Transactions */}
            <div className="card" style={{ padding: 20 }}>
              <div style={{ fontWeight: 700, marginBottom: 14, fontSize: 15, display: "flex", justifyContent: "space-between" }}>
                <span>Recent Activity</span>
                <button className="nav-btn" style={{ color: "#FF6B6B", fontSize: 13 }} onClick={() => setView("transactions")}>See all →</button>
              </div>
              {recentTx.slice(0, 5).map(tx => {
                const cat = getCat(tx.category);
                return (
                  <div key={tx.id} style={{ display: "flex", alignItems: "center", gap: 12, marginBottom: 14 }}>
                    <div style={{ width: 40, height: 40, borderRadius: 12, background: cat.color + "22", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 18, flexShrink: 0 }}>
                      {cat.icon}
                    </div>
                    <div style={{ flex: 1, minWidth: 0 }}>
                      <div style={{ fontSize: 14, fontWeight: 500, overflow: "hidden", textOverflow: "ellipsis", whiteSpace: "nowrap" }}>{tx.note || cat.label}</div>
                      <div style={{ fontSize: 12, color: "#555", marginTop: 1 }}>{new Date(tx.date).toLocaleDateString("en-US", { month: "short", day: "numeric" })}</div>
                    </div>
                    <div style={{ fontWeight: 700, fontSize: 15, color: tx.type === "income" ? "#4ECDC4" : tx.type === "savings" ? "#74B9FF" : "#FF6B6B", flexShrink: 0 }}>
                      {tx.type === "income" ? "+" : "-"}{formatCurrency(tx.amount)}
                    </div>
                  </div>
                );
              })}
            </div>

            {/* Quick Stats */}
            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12 }}>
              <div className="card" style={{ padding: 18 }}>
                <div style={{ color: "#555", fontSize: 12 }}>Daily Average</div>
                <div style={{ fontSize: 22, fontWeight: 700, color: "#FF6B6B", marginTop: 4 }}>
                  {formatCurrency(totalExpenses / (new Date().getDate() || 1))}
                </div>
                <div style={{ color: "#444", fontSize: 11, marginTop: 4 }}>per day this month</div>
              </div>
              <div className="card" style={{ padding: 18 }}>
                <div style={{ color: "#555", fontSize: 12 }}>Savings Rate</div>
                <div style={{ fontSize: 22, fontWeight: 700, color: "#74B9FF", marginTop: 4 }}>
                  {totalIncome > 0 ? Math.round((totalSavings / totalIncome) * 100) : 0}%
                </div>
                <div style={{ color: "#444", fontSize: 11, marginTop: 4 }}>of income saved</div>
              </div>
            </div>
          </div>
        )}

        {/* TRANSACTIONS */}
        {view === "transactions" && (
          <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
            <div style={{ color: "#555", fontSize: 13, marginBottom: 4 }}>{transactions.length} transactions total</div>
            {[...transactions].sort((a, b) => new Date(b.date) - new Date(a.date)).map(tx => {
              const cat = getCat(tx.category);
              return (
                <div key={tx.id} className="card" style={{ padding: 16, display: "flex", alignItems: "center", gap: 12 }}>
                  <div style={{ width: 44, height: 44, borderRadius: 14, background: cat.color + "22", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 20, flexShrink: 0 }}>
                    {cat.icon}
                  </div>
                  <div style={{ flex: 1, minWidth: 0 }}>
                    <div style={{ fontWeight: 500, fontSize: 14, overflow: "hidden", textOverflow: "ellipsis", whiteSpace: "nowrap" }}>{tx.note || cat.label}</div>
                    <div style={{ fontSize: 12, color: "#555", marginTop: 2 }}>
                      {cat.label} · {new Date(tx.date).toLocaleDateString("en-US", { month: "short", day: "numeric", year: "numeric" })}
                    </div>
                  </div>
                  <div style={{ textAlign: "right", flexShrink: 0 }}>
                    <div style={{ fontWeight: 700, fontSize: 15, color: tx.type === "income" ? "#4ECDC4" : tx.type === "savings" ? "#74B9FF" : "#F0EDE8" }}>
                      {tx.type === "income" ? "+" : "-"}{formatCurrency(tx.amount)}
                    </div>
                    <button onClick={() => deleteTransaction(tx.id)}
                      style={{ background: "none", border: "none", color: "#444", cursor: "pointer", fontSize: 11, marginTop: 2 }}>✕ remove</button>
                  </div>
                </div>
              );
            })}
          </div>
        )}

        {/* SAVINGS */}
        {view === "savings" && (
          <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
            <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
              <div style={{ color: "#555", fontSize: 13 }}>Your savings goals</div>
              <button className="btn" onClick={() => setGoalModal(true)}
                style={{ background: "#74B9FF22", color: "#74B9FF", border: "1px solid #74B9FF44", padding: "8px 14px", fontSize: 12 }}>
                + New Goal
              </button>
            </div>
            {savingsGoals.map(goal => {
              const pct = Math.min((goal.current / goal.target) * 100, 100);
              return (
                <div key={goal.id} className="card" style={{ padding: 22 }}>
                  <div style={{ display: "flex", alignItems: "center", gap: 14, marginBottom: 16 }}>
                    <div style={{ width: 52, height: 52, borderRadius: 16, background: goal.color + "22", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 24 }}>
                      {goal.icon}
                    </div>
                    <div style={{ flex: 1 }}>
                      <div style={{ fontWeight: 700, fontSize: 16 }}>{goal.name}</div>
                      <div style={{ color: "#555", fontSize: 13, marginTop: 2 }}>
                        {formatCurrency(goal.current)} of {formatCurrency(goal.target)}
                      </div>
                    </div>
                    <div style={{ textAlign: "right" }}>
                      <div style={{ fontFamily: "'Syne', sans-serif", fontSize: 22, fontWeight: 800, color: goal.color }}>{Math.round(pct)}%</div>
                    </div>
                  </div>
                  <div className="progress-bar" style={{ height: 8 }}>
                    <div className="progress-fill" style={{ width: `${pct}%`, background: `linear-gradient(90deg, ${goal.color}88, ${goal.color})` }} />
                  </div>
                  <div style={{ display: "flex", justifyContent: "space-between", marginTop: 10 }}>
                    <span style={{ color: "#555", fontSize: 12 }}>{formatCurrency(goal.target - goal.current)} remaining</span>
                    {pct >= 100 && <span style={{ color: "#4ECDC4", fontSize: 12, fontWeight: 600 }}>🎉 Goal reached!</span>}
                  </div>
                  <div style={{ display: "flex", gap: 8, marginTop: 14 }}>
                    <button className="btn" onClick={() => {
                      const amt = parseFloat(prompt("Add amount to savings:", "50"));
                      if (!isNaN(amt) && amt > 0) {
                        setSavingsGoals(prev => prev.map(g => g.id === goal.id ? { ...g, current: Math.min(g.current + amt, g.target) } : g));
                        const tx = { id: generateId(), type: "savings", category: "savings", amount: amt, note: `Saved for ${goal.name}`, date: new Date().toISOString() };
                        setTransactions(prev => [tx, ...prev]);
                      }
                    }}
                      style={{ background: goal.color + "22", color: goal.color, border: `1px solid ${goal.color}44`, padding: "8px 16px", fontSize: 13, flex: 1 }}>
                      + Add Funds
                    </button>
                    <button className="btn" onClick={() => setSavingsGoals(prev => prev.filter(g => g.id !== goal.id))}
                      style={{ background: "#FF6B6B11", color: "#FF6B6B", border: "1px solid #FF6B6B22", padding: "8px 16px", fontSize: 13 }}>
                      ✕
                    </button>
                  </div>
                </div>
              );
            })}
            {/* Savings Summary */}
            <div className="card" style={{ padding: 20, background: "linear-gradient(135deg, #74B9FF11, #0D0D0D)" }}>
              <div style={{ fontWeight: 700, marginBottom: 12 }}>Total Saved</div>
              <div style={{ fontFamily: "'Syne', sans-serif", fontSize: 36, fontWeight: 800, color: "#74B9FF" }}>
                {formatCurrency(savingsGoals.reduce((s, g) => s + g.current, 0))}
              </div>
              <div style={{ color: "#555", fontSize: 13, marginTop: 4 }}>
                across {savingsGoals.length} goals · targeting {formatCurrency(savingsGoals.reduce((s, g) => s + g.target, 0))}
              </div>
            </div>
          </div>
        )}

        {/* BUDGET */}
        {view === "budget" && (
          <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
            <div style={{ color: "#555", fontSize: 13, marginBottom: 4 }}>Monthly budget limits by category</div>
            {CATEGORIES.filter(c => c.id !== "savings" && c.id !== "other").map(cat => {
              const spent = expenseByCategory[cat.id] || 0;
              const limit = budget[cat.id] || 0;
              const pct = limit > 0 ? Math.min((spent / limit) * 100, 100) : 0;
              const over = spent > limit && limit > 0;
              return (
                <div key={cat.id} className="card" style={{ padding: 18, borderColor: over ? "#FF6B6B33" : "#2a2a2a" }}>
                  <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", marginBottom: 12 }}>
                    <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
                      <span style={{ fontSize: 22 }}>{cat.icon}</span>
                      <div>
                        <div style={{ fontWeight: 500, fontSize: 14 }}>{cat.label}</div>
                        <div style={{ fontSize: 12, color: over ? "#FF6B6B" : "#555" }}>
                          {formatCurrency(spent)} / {formatCurrency(limit)} {over && "⚠️ Over budget!"}
                        </div>
                      </div>
                    </div>
                    <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
                      <span style={{ color: "#555", fontSize: 13 }}>$</span>
                      <input type="number" value={limit}
                        onChange={e => setBudget(prev => ({ ...prev, [cat.id]: parseFloat(e.target.value) || 0 }))}
                        style={{ background: "#0D0D0D", border: "1px solid #2a2a2a", borderRadius: 8, color: "#F0EDE8", padding: "6px 10px", fontSize: 14, width: 90, outline: "none", textAlign: "right" }} />
                    </div>
                  </div>
                  <div className="progress-bar">
                    <div className="progress-fill" style={{ width: `${pct}%`, background: over ? "#FF6B6B" : pct > 70 ? "#FFB347" : cat.color }} />
                  </div>
                </div>
              );
            })}
            <div className="card" style={{ padding: 18, background: "#161616" }}>
              <div style={{ display: "flex", justifyContent: "space-between" }}>
                <span style={{ color: "#555", fontSize: 13 }}>Total Budget</span>
                <span style={{ fontWeight: 700 }}>{formatCurrency(Object.values(budget).reduce((s, v) => s + v, 0))}</span>
              </div>
              <div style={{ display: "flex", justifyContent: "space-between", marginTop: 8 }}>
                <span style={{ color: "#555", fontSize: 13 }}>Total Spent</span>
                <span style={{ fontWeight: 700, color: "#FF6B6B" }}>{formatCurrency(totalExpenses)}</span>
              </div>
              <div style={{ height: 1, background: "#2a2a2a", margin: "12px 0" }} />
              <div style={{ display: "flex", justifyContent: "space-between" }}>
                <span style={{ color: "#555", fontSize: 13 }}>Remaining</span>
                <span style={{ fontWeight: 700, color: "#4ECDC4" }}>{formatCurrency(Math.max(0, Object.values(budget).reduce((s, v) => s + v, 0) - totalExpenses))}</span>
              </div>
            </div>
          </div>
        )}
      </div>

      {/* Add Transaction Modal */}
      {addModal && (
        <div className="modal-bg" onClick={e => e.target === e.currentTarget && setAddModal(false)}>
          <div className="modal">
            <div style={{ fontFamily: "'Syne', sans-serif", fontWeight: 800, fontSize: 20, marginBottom: 20 }}>Add Transaction</div>
            {/* Type Toggle */}
            <div style={{ display: "flex", gap: 8, marginBottom: 16 }}>
              {[["expense","Expense","#FF6B6B"],["income","Income","#4ECDC4"],["savings","Savings","#74B9FF"]].map(([type, label, color]) => (
                <button key={type} onClick={() => setForm(f => ({ ...f, type }))}
                  style={{ flex: 1, padding: "10px", border: `1px solid ${form.type === type ? color : "#2a2a2a"}`, borderRadius: 12, background: form.type === type ? color + "22" : "transparent", color: form.type === type ? color : "#666", cursor: "pointer", fontWeight: 600, fontSize: 13 }}>
                  {label}
                </button>
              ))}
            </div>
            <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
              <select className="input" value={form.category} onChange={e => setForm(f => ({ ...f, category: e.target.value }))}>
                {CATEGORIES.map(cat => <option key={cat.id} value={cat.id}>{cat.icon} {cat.label}</option>)}
              </select>
              <input className="input" type="number" placeholder="Amount (e.g. 24.50)" value={form.amount} onChange={e => setForm(f => ({ ...f, amount: e.target.value }))} />
              <input className="input" type="text" placeholder="Note (optional)" value={form.note} onChange={e => setForm(f => ({ ...f, note: e.target.value }))} />
              <input className="input" type="date" value={form.date} onChange={e => setForm(f => ({ ...f, date: e.target.value }))} />
              <div style={{ display: "flex", gap: 10, marginTop: 4 }}>
                <button className="btn" onClick={() => setAddModal(false)}
                  style={{ flex: 1, padding: "14px", background: "transparent", border: "1px solid #2a2a2a", color: "#666", fontSize: 14 }}>Cancel</button>
                <button className="btn" onClick={addTransaction}
                  style={{ flex: 2, padding: "14px", background: "#FF6B6B", color: "white", fontSize: 14 }}>Add Transaction</button>
              </div>
            </div>
          </div>
        </div>
      )}

      {/* Add Goal Modal */}
      {goalModal && (
        <div className="modal-bg" onClick={e => e.target === e.currentTarget && setGoalModal(false)}>
          <div className="modal">
            <div style={{ fontFamily: "'Syne', sans-serif", fontWeight: 800, fontSize: 20, marginBottom: 20 }}>New Savings Goal</div>
            <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
              <input className="input" placeholder="Goal name (e.g. Dream Vacation)" value={goalForm.name} onChange={e => setGoalForm(f => ({ ...f, name: e.target.value }))} />
              <input className="input" type="number" placeholder="Target amount" value={goalForm.target} onChange={e => setGoalForm(f => ({ ...f, target: e.target.value }))} />
              <div style={{ display: "flex", gap: 8 }}>
                {["✈️","🏠","💻","🚗","🎓","💍","📱","⭐"].map(icon => (
                  <button key={icon} onClick={() => setGoalForm(f => ({ ...f, icon }))}
                    style={{ width: 40, height: 40, borderRadius: 10, border: `2px solid ${goalForm.icon === icon ? "#74B9FF" : "#2a2a2a"}`, background: goalForm.icon === icon ? "#74B9FF22" : "transparent", fontSize: 18, cursor: "pointer" }}>
                    {icon}
                  </button>
                ))}
              </div>
              <div style={{ display: "flex", gap: 8 }}>
                {["#FF6B6B","#4ECDC4","#FFE66D","#74B9FF","#C3A6FF","#A8E6CF"].map(color => (
                  <button key={color} onClick={() => setGoalForm(f => ({ ...f, color }))}
                    style={{ width: 32, height: 32, borderRadius: "50%", background: color, border: `3px solid ${goalForm.color === color ? "white" : "transparent"}`, cursor: "pointer" }} />
                ))}
              </div>
              <div style={{ display: "flex", gap: 10, marginTop: 4 }}>
                <button className="btn" onClick={() => setGoalModal(false)}
                  style={{ flex: 1, padding: "14px", background: "transparent", border: "1px solid #2a2a2a", color: "#666", fontSize: 14 }}>Cancel</button>
                <button className="btn" onClick={addGoal}
                  style={{ flex: 2, padding: "14px", background: "#74B9FF", color: "white", fontSize: 14 }}>Create Goal</button>
              </div>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}