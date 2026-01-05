# Desafio-Foursys
desafio foursys

import React, { useState } from 'react';
import { 
    Plus, Wallet, Heart, TrendingUp, ChevronRight, 
    ShieldCheck, FileDown, FileText, CheckCircle2, 
    User, Lock, Eye, EyeOff, LayoutPanelLeft 
} from 'lucide-react';

const employees = [
    { id: '1', name: 'Ricardo Santos', role: 'Dev Full Stack', status: 'active', salary: 8500, avatar: 'https://picsum.photos/40/40?random=1' },
    { id: '2', name: 'Mariana Oliveira', role: 'Product Designer', status: 'active', salary: 7200, avatar: 'https://picsum.photos/40/40?random=2' },
    { id: '3', name: 'Ana Beatriz', role: 'Atendimento', status: 'active', salary: 3200, avatar: 'https://picsum.photos/40/40?random=3' },
];

const HRManager: React.FC = () => {
    // Simulação de autenticação: 'admin' ou 'employee'
    const [viewMode, setViewMode] = useState<'admin' | 'employee'>('admin');
    const [extracting, setExtracting] = useState(false);

    // Dados do colaborador logado (simulado)
    const currentUser = employees[0]; 

    const handleExtract = () => {
        setExtracting(true);
        setTimeout(() => {
            setExtracting(false);
            alert("Seu holerite foi extraído com sucesso e enviado para seu e-mail cadastrado.");
        }, 1500);
    };

    return (
        <div className="max-w-6xl mx-auto space-y-8 animate-in fade-in slide-in-from-bottom-4 duration-500">
            {/* Header com Switcher de Visão para Demo */}
            <div className="flex flex-col md:flex-row md:items-center justify-between gap-6 bg-white/5 p-6 rounded-[2rem] border border-white/10">
                <div className="flex items-center gap-4">
                    <div className="w-12 h-12 rounded-2xl bg-blue-600/20 flex items-center justify-center text-blue-400 border border-blue-500/20">
                        {viewMode === 'admin' ? <ShieldCheck size={24} /> : <User size={24} />}
                    </div>
                    <div>
                        <h3 className="text-xl font-bold text-slate-100">
                            {viewMode === 'admin' ? 'Gestão de RH (Admin)' : 'Meu Portal do Colaborador'}
                        </h3>
                        <p className="text-sm text-slate-400">
                            {viewMode === 'admin' ? 'Controle total da folha e time.' : 'Acesse seus documentos e benefícios com segurança.'}
                        </p>
                    </div>
                </div>

                <div className="flex items-center bg-slate-900 rounded-2xl p-1 border border-white/5">
                    <button 
                        onClick={() => setViewMode('admin')}
                        className={`px-4 py-2 rounded-xl text-xs font-bold transition-all flex items-center gap-2 ${viewMode === 'admin' ? 'bg-blue-600 text-white shadow-lg' : 'text-slate-500 hover:text-slate-300'}`}
                    >
                        <LayoutPanelLeft size={14} /> Visão Empresa
                    </button>
                    <button 
                        onClick={() => setViewMode('employee')}
                        className={`px-4 py-2 rounded-xl text-xs font-bold transition-all flex items-center gap-2 ${viewMode === 'employee' ? 'bg-blue-600 text-white shadow-lg' : 'text-slate-500 hover:text-slate-300'}`}
                    >
                        <User size={14} /> Meu Acesso
                    </button>
                </div>
            </div>

            {viewMode === 'admin' ? (
                /* --- VISÃO ADMINISTRADOR --- */
                <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <div className="lg:col-span-2 space-y-6">
                        <div className="bg-white/5 rounded-3xl border border-white/10 overflow-hidden shadow-sm">
                            <div className="p-6 border-b border-white/10 flex items-center justify-between bg-white/5">
                                <h4 className="font-bold text-slate-200">Gestão de Folha - Time Ativo</h4>
                                <button className="px-4 py-2 bg-blue-600 hover:bg-blue-700 text-white rounded-xl text-xs font-bold flex items-center gap-2 transition-all">
                                    <Plus size={14} /> Nova Contratação
                                </button>
                            </div>
                            <div className="overflow-x-auto">
                                <table className="w-full text-left">
                                    <thead>
                                        <tr className="bg-white/5 text-[10px] uppercase tracking-widest font-bold text-slate-500">
                                            <th className="px-6 py-4">Colaborador</th>
                                            <th className="px-6 py-4">Status</th>
                                            <th className="px-6 py-4">Salário Base</th>
                                            <th className="px-6 py-4 text-right">Ações</th>
                                        </tr>
                                    </thead>
                                    <tbody className="divide-y divide-white/5">
                                        {employees.map(emp => (
                                            <tr key={emp.id} className="hover:bg-white/5 transition-colors group">
                                                <td className="px-6 py-4 flex items-center gap-3">
                                                    <img src={emp.avatar} className="w-8 h-8 rounded-full border border-white/10" alt="" />
                                                    <div>
                                                        <p className="text-sm font-bold text-slate-200">{emp.name}</p>
                                                        <p className="text-[10px] text-slate-500 uppercase">{emp.role}</p>
                                                    </div>
                                                </td>
                                                <td className="px-6 py-4">
                                                    <span className="px-2 py-0.5 rounded-full bg-emerald-500/10 text-emerald-400 text-[10px] font-bold uppercase">Ativo</span>
                                                </td>
                                                <td className="px-6 py-4 text-sm font-medium text-slate-200">
                                                    R$ {emp.salary.toLocaleString('pt-BR')}
                                                </td>
                                                <td className="px-6 py-4 text-right">
                                                    <button className="p-2 hover:bg-white/10 rounded-lg text-slate-500 transition-colors">
                                                        <ChevronRight size={18} />
                                                    </button>
                                                </td>
                                            </tr>
                                        ))}
                                    </tbody>
                                </table>
                            </div>
                        </div>

                        <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div className="bg-white/5 p-6 rounded-3xl border border-white/10 flex items-center gap-4">
                                <div className="w-12 h-12 rounded-2xl bg-indigo-600/10 text-indigo-400 flex items-center justify-center">
                                    <TrendingUp size={24} />
                                </div>
                                <div>
                                    <h5 className="font-bold text-slate-200 text-sm">Turnover</h5>
                                    <p className="text-xl font-black text-white">4.2%</p>
                                </div>
                            </div>
                            <div className="bg-white/5 p-6 rounded-3xl border border-white/10 flex items-center gap-4">
                                <div className="w-12 h-12 rounded-2xl bg-emerald-600/10 text-emerald-400 flex items-center justify-center">
                                    <CheckCircle2 size={24} />
                                </div>
                                <div>
                                    <h5 className="font-bold text-slate-200 text-sm">Folha Validada</h5>
                                    <p className="text-sm text-slate-400 italic">Pronta p/ Junho</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div className="space-y-6">
                        <div className="bg-white/5 p-6 rounded-3xl border border-white/10">
                            <h4 className="font-bold text-slate-200 mb-6 flex justify-between">
                                Resumo Financeiro RH
                                <Lock size={16} className="text-slate-500" />
                            </h4>
                            <div className="space-y-4">
                                <div className="flex justify-between text-sm">
                                    <span className="text-slate-500">Salários Brutos</span>
                                    <span className="font-bold text-slate-200">R$ 18.900,00</span>
                                </div>
                                <div className="flex justify-between text-sm">
                                    <span className="text-slate-500">Encargos/Impostos</span>
                                    <span className="font-bold text-slate-200">R$ 5.670,00</span>
                                </div>
                                <div className="h-px bg-white/10"></div>
                                <div className="flex justify-between text-lg font-black text-blue-400">
                                    <span>Total</span>
                                    <span>R$ 24.570,00</span>
                                </div>
                            </div>
                            <button className="w-full mt-6 py-4 bg-emerald-600 hover:bg-emerald-700 text-white rounded-2xl font-bold transition-all">
                                Agendar Todos Pagamentos
                            </button>
                        </div>
                    </div>
                </div>
            ) : (
                /* --- VISÃO COLABORADOR (RESTRITA) --- */
                <div className="grid grid-cols-1 lg:grid-cols-12 gap-8 animate-in zoom-in-95 duration-300">
                    <div className="lg:col-span-8 space-y-8">
                        {/* Perfil Header */}
                        <div className="bg-gradient-to-br from-blue-600/10 to-transparent p-8 rounded-[2.5rem] border border-blue-500/20 flex flex-col md:flex-row items-center gap-8">
                            <div className="relative">
                                <img src={currentUser.avatar} className="w-32 h-32 rounded-3xl border-4 border-blue-600/20 shadow-2xl" alt="" />
                                <div className="absolute -bottom-2 -right-2 bg-emerald-500 p-2 rounded-xl shadow-lg">
                                    <CheckCircle2 size={16} className="text-white" />
                                </div>
                            </div>
                            <div className="text-center md:text-left space-y-2">
                                <h2 className="text-3xl font-black text-white">{currentUser.name}</h2>
                                <p className="text-blue-400 font-bold uppercase tracking-widest text-sm">{currentUser.role}</p>
                                <div className="flex items-center justify-center md:justify-start gap-4 pt-2">
                                    <div className="px-3 py-1 bg-white/5 border border-white/10 rounded-lg text-xs text-slate-400">ID: #8842-X</div>
                                    <div className="px-3 py-1 bg-white/5 border border-white/10 rounded-lg text-xs text-slate-400">Desde: Jan/2023</div>
                                </div>
                            </div>
                        </div>

                        {/* Holerite Section */}
                        <div className="bg-white/5 rounded-3xl border border-white/10 overflow-hidden">
                            <div className="p-8 flex flex-col md:flex-row items-center justify-between gap-6">
                                <div className="space-y-2 text-center md:text-left">
                                    <div className="inline-flex items-center gap-2 text-emerald-400 text-xs font-bold uppercase tracking-widest mb-2">
                                        <FileCheck2 size={16} className="text-emerald-400" />
                                        Disponível para Extração
                                    </div>
                                    <h4 className="text-2xl font-bold text-white">Holerite Mensal - Maio/2024</h4>
                                    <p className="text-slate-400 max-w-sm">Seu demonstrativo de pagamento foi gerado e validado pelo departamento financeiro.</p>
                                </div>
                                <button 
                                    onClick={handleExtract}
                                    disabled={extracting}
                                    className="px-10 py-5 bg-blue-600 hover:bg-blue-500 text-white rounded-2xl font-black text-lg transition-all shadow-xl shadow-blue-900/40 flex items-center gap-3 disabled:opacity-50 group"
                                >
                                    {extracting ? 'Processando...' : (
                                        <>
                                            <FileDown size={24} className="group-hover:translate-y-1 transition-transform" />
                                            Extrair Meu Holerite
                                        </>
                                    )}
                                </button>
                            </div>
                            <div className="px-8 py-4 bg-white/[0.02] border-t border-white/5 flex items-center justify-center md:justify-start gap-6 text-[10px] font-bold text-slate-500 uppercase tracking-widest">
                                <span className="flex items-center gap-1"><Lock size={12} /> Criptografia Ponta-a-Ponta</span>
                                <span className="flex items-center gap-1"><ShieldCheck size={12} /> Assinado Digitalmente</span>
                            </div>
                        </div>

                        <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div className="bg-white/5 p-8 rounded-[2rem] border border-white/10 space-y-4 group hover:bg-white/[0.07] transition-all cursor-pointer">
                                <div className="w-12 h-12 bg-pink-600/20 text-pink-400 rounded-2xl flex items-center justify-center">
                                    <Heart size={24} />
                                </div>
                                <div>
                                    <h5 className="font-bold text-white text-lg">Meus Benefícios</h5>
                                    <p className="text-sm text-slate-500">Plano Bradesco Saúde & VR Alimentação</p>
                                </div>
                                <div className="flex justify-between items-center pt-2">
                                    <span className="text-xs font-bold text-slate-300">Status: Ativo</span>
                                    <ChevronRight size={16} className="text-slate-600" />
                                </div>
                            </div>
                            <div className="bg-white/5 p-8 rounded-[2rem] border border-white/10 space-y-4 group hover:bg-white/[0.07] transition-all cursor-pointer">
                                <div className="w-12 h-12 bg-blue-600/20 text-blue-400 rounded-2xl flex items-center justify-center">
                                    <Wallet size={24} />
                                </div>
                                <div>
                                    <h5 className="font-bold text-white text-lg">Crédito Consignado</h5>
                                    <p className="text-sm text-slate-500">Simule um empréstimo com taxas do banco.</p>
                                </div>
                                <div className="flex justify-between items-center pt-2">
                                    <span className="text-xs font-bold text-blue-400">Liberado: R$ 15.000</span>
                                    <ChevronRight size={16} className="text-slate-600" />
                                </div>
                            </div>
                        </div>
                    </div>

                    <div className="lg:col-span-4 space-y-6">
                        <div className="bg-white/5 p-8 rounded-[2.5rem] border border-white/10 space-y-6">
                            <h4 className="font-bold text-slate-200 flex items-center gap-2">
                                <History size={18} className="text-slate-500" />
                                Histórico de Pagamentos
                            </h4>
                            <div className="space-y-4">
                                {[
                                    { month: 'Abril', year: '2024', status: 'pago' },
                                    { month: 'Março', year: '2024', status: 'pago' },
                                    { month: 'Fevereiro', year: '2024', status: 'pago' },
                                ].map((doc, i) => (
                                    <div key={i} className="flex items-center justify-between p-4 bg-white/5 rounded-2xl border border-white/5 hover:bg-white/10 transition-all cursor-pointer group">
                                        <div className="flex items-center gap-3">
                                            <FileText size={18} className="text-slate-500 group-hover:text-blue-400" />
                                            <div>
                                                <p className="text-sm font-bold text-slate-200">{doc.month}/{doc.year}</p>
                                                <p className="text-[10px] text-emerald-400 uppercase font-black tracking-tighter">Liquidado</p>
                                            </div>
                                        </div>
                                        <FileDown size={16} className="text-slate-600 group-hover:text-white" />
                                    </div>
                                ))}
                            </div>
                            <button className="w-full py-4 border border-white/10 text-slate-400 rounded-2xl text-xs font-bold uppercase tracking-widest hover:bg-white/5 transition-all">
                                Ver Todo Histórico
                            </button>
                        </div>

                        <div className="bg-gradient-to-br from-slate-800 to-slate-900 p-8 rounded-[2.5rem] border border-white/10 text-center space-y-4">
                            <div className="w-16 h-16 bg-blue-600/20 text-blue-400 rounded-3xl flex items-center justify-center mx-auto mb-2">
                                <Lock size={32} />
                            </div>
                            <h5 className="font-bold text-white">Privacidade de Dados</h5>
                            <p className="text-xs text-slate-400 leading-relaxed">
                                Seus dados salariais são sigilosos e visíveis apenas para você e o RH autorizado. Ninguém mais no time pode acessar estas informações.
                            </p>
                        </div>
                    </div>
                </div>
            )}
        </div>
    );
};

// Subcomponentes extras para ícones que faltaram
const FileCheck2 = ({size, className}: {size: number, className: string}) => (
    <svg xmlns="http://www.w3.org/2000/svg" width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"/><polyline points="14 2 14 8 20 8"/><path d="m9 15 2 2 4-4"/></svg>
);
const History = ({size, className}: {size: number, className: string}) => (
    <svg xmlns="http://www.w3.org/2000/svg" width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M3 12a9 9 0 1 0 9-9 9.75 9.75 0 0 0-6.74 2.74L3 8"/><path d="M3 3v5h5"/><path d="M12 7v5l4 2"/></svg>
);

export default HRManager;
