<%*
const mermaidCode = `
graph TD;
    A[Start] --> B{Decision?};
    B -->|Yes| C[Do something];
    B -->|No| D[Do nothing];
`;
tR += `\n\`\`\`mermaid\n${mermaidCode}\n\`\`\`\n`;
%>
