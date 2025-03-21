import { useEffect, useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Table, TableHead, TableRow, TableHeaderCell, TableBody, TableCell } from "@/components/ui/table";
import { Button } from "@/components/ui/button";

export default function CRMTable() {
  const [leads, setLeads] = useState([]);

  useEffect(() => {
    fetch("http://localhost:8000/leads/")
      .then((response) => response.json())
      .then((data) => setLeads(data));
  }, []);

  return (
    <div className="container mx-auto p-4">
      <Card>
        <CardContent>
          <h2 className="text-xl font-bold mb-4">Лиды</h2>
          <Table>
            <TableHead>
              <TableRow>
                <TableHeaderCell>ID</TableHeaderCell>
                <TableHeaderCell>Имя</TableHeaderCell>
                <TableHeaderCell>Телефон</TableHeaderCell>
                <TableHeaderCell>Email</TableHeaderCell>
                <TableHeaderCell>Бюджет</TableHeaderCell>
                <TableHeaderCell>Источник</TableHeaderCell>
                <TableHeaderCell>Статус</TableHeaderCell>
                <TableHeaderCell>Действия</TableHeaderCell>
              </TableRow>
            </TableHead>
            <TableBody>
              {leads.map((lead) => (
                <TableRow key={lead.id}>
                  <TableCell>{lead.id}</TableCell>
                  <TableCell>{lead.name}</TableCell>
                  <TableCell>{lead.phone}</TableCell>
                  <TableCell>{lead.email || "-"}</TableCell>
                  <TableCell>{lead.budget || "-"}</TableCell>
                  <TableCell>{lead.source || "-"}</TableCell>
                  <TableCell>{lead.status}</TableCell>
                  <TableCell>
                    <Button variant="outline">Изменить</Button>
                    <Button variant="destructive" className="ml-2">Удалить</Button>
                  </TableCell>
                </TableRow>
              ))}
            </TableBody>
          </Table>
        </CardContent>
      </Card>
    </div>
  );
}
